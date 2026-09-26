---
# 必填。项目名称。
title: "从Chrome源码看JS Array的实现"
# 可选，和文章一样使用。
slug: 从Chrome源码看JS Array的实现
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2019-08-01
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: false
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "从Chrome源码看JS Array的实现:JS Array的实现,Push和扩容,Pop和减容,shift和splice数组中间的操作,Join和Sort,Array和线性链接的速度"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Javascript
tags:
  - 源码
  - Javascript
  - JS
  - Array
  - pop
  - shift
  - splice
  - join
  - sort
  - array
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

### 从Chrome源码看JS Array的实现

> JS的Array是一个万能的数据结构，为什么这么说呢？因为首先它可以当作一个普通的数组来使用，即通过下标找到数组的元素：

  ```js
  var ary = [19, 59, 99]
  console.log(ary[0]) // 19
  ```

> 然后它可以当作一个栈来使用，我们知道栈的特点是先进后出，栈的基本操作是出栈和入栈：

  ```js
  var ary = [1, 2, 3]
  ary.push(4) // 入栈
  ary.pop() // 出栈
  ```

> 同时它还可以当作一个队列，队列的特点是先进先出，基本操作是出队和入队：

  ```js
  var ary = [1, 2, 3]
  ary.push(4) // 入队
  ary.shift() // 出队
  ```

> 甚至它还可以当作一个哈希表来使用(但是不推荐这么用)：

  ```js
  var ary = [1, 2, 3, 4]
  // 从第3个元素开始，删掉1个元素，并插入-1，-2这两个元素
  ary.splice(2, 1, -1, -2) // [1, 2, -1, -2, 4]
  // 再来个2000的索引
  ary[2000] = 2000 // [1, 2, -1, -2, 4, empty*1995, 2000]
  ```

> JS Array一方面提供了很大的便利，只要用一个数据结构就可以做很多事情，使用者不需要关心各者的区别，使得JS很容易入门。另一方面它屏蔽了数据结构的概念，不少写前端的都不知道什么是栈、队列、哈希、树，特别是那些不是学计算机，中途转过来的。然而这往往是不可取的。

> 另外一点是，即使是一些前端的老司机，他们也很难说清楚，这些数组函数操作的效率怎么样，例如说随意地往数组中间增加一个元素不会有性能问题么。所以就很有必要从源码的角度看一下数组是怎么实现的。


#### 1. JS Array的实现

> 先看源码注释：

  ```js
  // The JSArray describes JavaScript Arrays
  //  Such an array can be in one of two modes:
  //    - fast, backing storage is a FixedArray and length <= elements.length();
  //       Please note: push and pop can be used to grow and shrink the array.
  //    - slow, backing storage is a HashTable with numbers as keys.
  class JSArray: public JSObject {
    public:
    // [length]: The length property.
    DECL_ACCESSORS (length, Object) 

    // Number of element slots to pre-allocate for an empty array.
    static const int kPreallocatedArrayElements = 4;
  };
  ```

  - 这里说明一下，如果不熟悉C/C++的，那把它成伪码就好了。
  - 源码里面说了，JSArray有两种模式，一种是快速的，一种是慢速的，快速的用的是索引直接定位，慢速的使用用哈希查找，由于JSArray是继承于JSObject，所以它也是同样的处理方式，如下面的：

    ```js
    var ary = [1, 2, 3]
    ary[2000] = 5
    ```

    - 增加一个2000的索引时，array就会被转成慢元素。

#### 2. Push和扩容

> 数组初始化大小为4：

  ```js
  // Number of element slots to pre-allocate for an empty array.
  static const int kPreallocatedArrayElements = 4;
  ```

  - 执行push的时候会在数组的末尾添加新的元素，而一旦空间不足时，将进行扩容。
  - 在源码里面push是用汇编实现的，在C++里面嵌入的汇编。这个应该是考虑到push是一个最为常用的操作，所以用汇编实现提高执行速度。在汇编的上面封装了一层，用C++调的封装的汇编的函数，在编译组装的时候，将把这些C++代码转成汇编代码。
  - 计算新容量的函数：

    ```js
    Node* CodeStubAssembler::CalculateNewElementsCapacity(Node* old_capacity, ParameterMode mode) {
      Node* half_old_capacity = WordOrSmiShr(old_capacity, 1, mode);
      Node* new_capacity = IntPtrOrSmiAdd(half_old_capacity, old_capacity, mode);
      Node* padding = IntPtrOrSmiConstant(16, mode);
      return IntPtrOrSmiAdd(new_capacity, padding, mode);
    }
    ```

    - 如上代码新容量等于 ：

      ```js
      new_capacity = old_capacity / 2 + old_capacity + 16
      ```

        - 即老的容量的1.5倍加上16。初始化为4个，当push第5个的时候，容量将会变成：

        ```js
        new_capacity = 4 / 2 + 4 + 16 = 22
        ```

      - 接着申请一块这么大的内存，把老的数据拷过去：

        ```js
        Node* CodeStubAssembler::GrowElementsCapacity(Node* object, Node* elements, Node* capacity, Node* new_capacity) {
          // Allocate the new backing store.
          Node* new_elements = AllocateFixedArray(new_capacity, mode);

          // Copy the elements from the old elements store to the new.
          CopyFixedArrayElements(elements, new_elements, capacity, new_capacity);
          return new_elements;
        }
        ```

        - 由于复制是用的memcopy，把整一段内存空间拷贝过去，所以这个操作还是比较快的。
        - 再把新元素放到当前length的位置，再把length增加1：

          ```js
          StoreFixedArrayElement(elements, var_length.value());
          Increment(var_length, 1, mode);
          ```

#### 3. Pop和减容

> push是用汇编实现，而pop的逻辑是用C++写的。在执行pop的时候，第一步，获取到当前的length，用这个length - 1得到要删除的元素，然后调用setLength调整容量，最后返回删除的元素：

  ```js
  int new_length = length - 1;
  int remove_index = remove_position == AT_START ? 0 : new_length;
  Handle<Object> result = Subclass::GetImpl(isolate, *backing_store, remove_index);
  Subclass::SetLengthImpl(isolate, receiver, new_length, backing_store);
  return result;
  ```

  - 我们重点看下这个减容的过程：

    ```js
    if (2 * length <= capacity) {
      // If more than half the elements won't be used, trim the array.
      isolate->heap()->RightTrimFixedArray(backing_store, capacity - length);
    } else {
      // Otherwise, fill the unused tail with holes.
      BackingStore::cast(*backing_store)->FillWithHoles(length, old_length);
    }
    ```

    - 如果容量大于等于length的2倍，则进行容量调整，否则用holes对象填充。第三行的rightTrim函数，会算出需要释放的空间大小，并做标记，并等待GC回收：

    ```js
    int bytes_to_trim = elements_to_trim * element_size;
    // Calculate location of new array end.
    Address old_end = object->address() + object->Size();
    Address new_end = old_end - bytes_to_trim;
    CreateFillerObjectAt(new_end, bytes_to_trim, ClearRecordedSlots::kYes);
    ```

    - 也就是说，当数组的元素个数小于容量的一半时，就会进行减少的操作，将容量调整为实际的大小。

#### 4. shift和splice数组中间的操作

> push和pop都是在数组末尾操作，相对比较简单，而shfit、unshfit、splice是在数组的开始或者中间进行操纵。我们来看一下，如果是这种情况的又是如何调整数组元素的。

  ##### （1）shift
    
  - shift是出队，即删除并返回数组的第一个元素。shift和pop调的都是同样的删除函数，只不过shift传的删除的postion是AT_STRT，源码里面会判断如果是AT_START的话，会把元素进行移动：
  
    ```js
    if (remove_position == AT_START) {
      Subclass::MoveElements(isolate, receiver, backing_store, 0, 1, new_length, 0, 0);
    }
    ```

  - 从1的位置移到0的位置，如上面第2行的第4、5个参数，这个move将会调leftTrim，和上面的rightTrim相反：

      ```js
      *dst_elms.location() = BackingStore::cast(heap->LeftTrimFixedArray(*dst_elms, src_index));
      receiver->set_elements(*dst_elms);
      ```
  
  ##### （2）unshfit
  
  - unshfit在数组的开始位置插入元素，首先要判断容量是否足够存放，如果不够，将容量扩展为老容量的1.5倍加16，然后把老元素移到新的内存空间偏移为unshift元素个数的位置，也就是说要腾出起始的空间放unshfit传进来的元素，如果空间足够了，则直接执行memmove移动内存空间，最后再把unshif传进来的参数copy到开始的位置，并更新array的length：
  
      ```js
      int insertion_index = add_position == AT_START ? 0 : length;
      // Copy the arguments to the start.
      Subclass::CopyArguments(args, backing_store, add_size, 1, insertion_index);
      // Set the length.
      receiver->set_length(Smi::FromInt(new_length));
      ```

  ##### （3）splice
  
  - splice的操作已经几乎不用去看源码了，通过shift和unshift的操作是怎么样的，就可以想象到它的执行过程是怎样的，只是shift/unshfit操作的index是0，而splice可以指定index。具体代码如下：

    ```js
    // Delete and move elements to make space for add_count new elements.
    if (add_count < delete_count) {
      Subclass::SpliceShrinkStep(isolate, receiver, backing_store, start, delete_count, add_count, length, new_length);
    } else if (add_count > delete_count) {
      backing_store = Subclass::SpliceGrowStep(isolate, receiver, backing_store, start, delete_count, add_count, length, new_length);
    }

    // Copy over the arguments.
    Subclass::CopyArguments(args, backing_store, add_count, 3, start);
    ```

    - 它需要先shrink或者grow中间元素的空间，以适应增加元素比删除元素少或者多的情况，然后进行容量调整和移动元素。

#### 5. Join和Sort

> 它们是用JS实现的，然后再用wasm打包成native code。不过，join的实现逻辑并不简单，因为array的元素本身具有多样化，可能为慢元素或者快元素，还可能带有循环引用，对于慢元素，需要先排下序：

  ```js
  var keys = GetSortedArrayKeys(array, %GetArrayKeys(array, length));
  ```

  - 预处理完之后，最后创建一个字符串数组，用连接符连起来：

    ```js
    // Construct an array for the elements.
    var elements = new InternalArray(length);
    for (var i = 0; i < length; i++) {
      elements[i] = ConvertToString(use_locale, array[i]);
    }

    if (separator === '') {
      return %StringBuilderConcat(elements, length, '');
    } else {
      return %StringBuilderJoin(elements, length, separator);
    }
    ```

  - 而sort函数是用的快速排序：

    ```js
    function ArraySort(comparefn) {
      CHECK_OBJECT_COERCIBLE(this, "Array.prototype.sort");
      %Log("js/array.js execute ArraySort");  //手动添加的log打印，确保执行的是这里

      var array = TO_OBJECT(this);
      var length = TO_LENGTH(array.length);
      return InnerArraySort(array, length, comparefn);
    }
    ```

    - 当数组元素的个数不超过10个时，是用的插入排序：

      ```js
      function InnerArraySort(array, length, comparefn) {
        // In-place QuickSort algorithm.
        // For short (length <= 10) arrays, insertion sort is used for efficiency.
        function QuickSort(a, from, to) {
          var third_index = 0;
          while (true) {
            // Insertion sort is faster for short arrays.
            if (to - from <= 10) {
              InsertionSort(a, from, to);
              return;
            }
            //other code ...
          }
        }
      }
      ```

    - 快速排序算法里面有一个比较重要的地方是选择枢纽元素，最简单的是每次都是选取第一个元素，或者中间的元素，在源码里面是这样选择的：

      ```js
      if (to - from > 1000) {
        third_index = GetThirdIndex(a, from, to);
      } else {
        third_index = from + ((to - from) >> 1);
      }
      ```

      - 如果元素个数在1000以内，则使用它们的中间元素，否则要算一下， 这个算法比较有趣：

        ```js
        function GetThirdIndex(a, from, to) { 
          var t_array = new InternalArray();
          // Use both 'from' and 'to' to determine the pivot candidates.
          var increment = 200 + ((to - from) & 15);
          var j = 0;
          from += 1;
          to -= 1;
          for (var i = from; i < to; i += increment) {
            t_array[j] = [i, a[i]];
            j++;
          }
          t_array.sort(function(a, b) {
            return comparefn(a[1], b[1]);
          });
          var third_index = t_array[t_array.length >> 1][0];
          return third_index;
        }
        ```

        - 先取一个递增间距200~215之间，再循环取出原元素里面落到这个间距的元素，放到一个新的数组里面（这个数组是C++里面的数组），然后排下序，取中间的元素。因为枢纽元素的刚好是所有元素的中位数时，排序的效果最好，而这里是取出少数元素的中位数，类似于抽样模拟，缺点是它得再借助另外的排序算法。
        - 最后再比较一下Array和线性链接的速度。

#### Array和线性链接的速度

> 线性链接是一种非连续存储的数据结构，每个元素都有一个指针指向它的下一个元素，所以它删除元素的时候不需要移动其它元素，也不需要考虑扩容的事情，但是它的查找比较慢。我们实现一个简单的List和Array进行比较。

- List的每个节点用一个Node表示：

  ```js
  class Node{
    constructor(value, next){
        this.value = value;
        this.next = next;
    }
  }
  ```

- 每个List都有一个头指针指向第一个元素，和一个length记录它的长度：

  ```js
  class List{
    constructor(){
        this.head = null;
        this.tail = null;
        this.length = 0;
    }
  }
  ```

- 然后实现它的push和unshift函数：

  ```js
  class List{
    unshift(value){
        return this.insert(0, value);
    }
    push(value){
        if(this.head === null){
            this.head = new Node(value, this.tail);
            this.length++;
        } else {
            this.insert(this.length, value);
        }
        return this.length;
    }
  }
  ```

- 两个函数都会调一个通用的insert函数：

  ```js
  insert(index, value){
    var insertPos = this.head;
    //找到需要插入的位置的节点
    for(var i = 0; i < index - 1; i++){
        insertPos = insertPos.next;
    }
    var node = null;
    if(index === 0){
        node = new Node(value, this.head);
        this.head = node;
    } else {
        node = new Node(value, insertPos.next);
        insertPos.next = node;
    }
    this.length++;
    return value;
  }
  ```

- 有了这个List之后，就可以初始化一个list和array：
  
  ```js
  var list = new List();
  var arr = [];
  for(var i = 0; i < 100; i++){
      list.push(i);
      arr.push(i);
  }
  ```

- 然后用下面的代码比较List和Array在数组起始位置插入元素的操作时间：

  ```js
  var count = 10000;
  console.time("list unshfit");
  for(var i = 0; i < count; i++){
      list.unshift(i);
  }
  console.timeEnd("list unshfit");

  console.time("array unshfit");
  for(var i = 0; i < count; i++){
      arr.unshift(i);
  }
  console.timeEnd("array unshfit");
  ```

- 再比较从正中间位置插入元素的时间：
  
  ```js
  console.time("list insert middle with index");
  for(var i = 0; i < count; i++){
      insertPos = list.insert(list.length >> 1, i);
  }
  console.timeEnd("list insert middle with index");

  console.time("array insert middle");
  for(var i = 0; i < count; i++){
      arr.splice(arr.length >> 1, 0, i);
  }
  console.timeEnd("array insert middle");
  ```

  - 运行可以得到以下表格：

    ||unshift|splice(n/2)|
    |----|----|----|
    |Array|350ms|7.99ms|
    |List|8.23ms|106ms|

    - 可以看到在队首插入元素，使用线性链接List的时间将会数量级的优于Array。如果是在中间位置插入的话，由于 List的查找花费了很多时间，导致总时间明显高于Array。但是如果在插入的时候，记住上一次的位置，那么List又会明显快于Array。如下换成记录插入的位置：

      ```js
      console.time("list insert middle with pos");
      var insertPos = list.getNode(list.length >> 1);
      for(var i = 0; i < count; i++){
          insertPos = list.insertFromNode(insertPos, i);
      }
      console.timeEnd("list insert middle with pos");
      ```

      - 时间比较List又快于Array：

        ||unshift|splice(n/2)|splice pos|
        |----|----|----|----|
        |Array|350ms|7.99ms|8.07ms|
        |List|8.23ms|106ms|1.78ms|

- 综上，Array的实现用了三种语言：汇编、C++和JS，最常用的如push用了汇编实现，比较常用的如pop/splice等用了C++，较为少用的如join/sort用了JS。

- Array为快元素即普通的数组时，增删元素操作需要不断的扩容、减容和调整元素的位置。特别是当不断地在起始位置插入元素时，和链表相比，这种时间效率还是比较低下的。如果使用的场景是要根据index删除元素，使用Array还是有优势，但是若能够很快定位到删除元素的位置，链表毫无疑问是更合适的。

- 【转载】原文地址：[https://zhuanlan.zhihu.com/p/26388217?utm_source=weibo&utm_medium=social](https://zhuanlan.zhihu.com/p/26388217?utm_source=weibo&utm_medium=social)
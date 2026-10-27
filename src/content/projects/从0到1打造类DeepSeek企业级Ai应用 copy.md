---
# 必填。项目名称。
title: "从0到1打造类DeepSeek企业级Ai应用"
# 可选，和文章一样使用。
slug: 类DeepSeek企业级网页版体验Ai应用
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2026-10-18
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: true
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 100
# 可选。卡片简介 + 详情页描述。
description: "本项目旨在构造一款高度复刻DeepSeek网页版体验的Ai对话工具。系统核心内容包括流式对话、深度推理（思维链展示）、实时联网搜索，并提供全量的用户历史会话管理和 全局/局部对话搜索 功能。系统满足高并发响应，且具备良好的可扩展性。"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
image: ""
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "planning"
# 分类
# category：Ai
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link:
#   - label: "GitHub"
#     icon: "fa7-brands:github"
#     value: "https://github.com/CuteLeaf/Firefly"
#   - label: "文档"
#     icon: "material-symbols:menu-book"
#     value: "https://docs-firefly.cuteleaf.cn"
# 可选。页面语言，如 zh_CN。
lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
tags:
  - Ai
---

<!-- ## 项目展示页使用指南

在 `src/content/projects/` 下新建一个 `.md` 或 `.mdx` 文件即可创建一个项目。**正文就是项目 README**，渲染在详情页底部；**frontmatter** 里的字段则用于列表卡片与详情页顶部展示。

## Frontmatter 字段

| 字段 | 类型 | 说明 |
|---|---|---|
| `title` | string | 必填。项目名称。 |
| `slug` | string | 可选，和文章一样使用。 |
| `published` | date | 必填。发布/更新日期，如 `2025-10-01`。用于排序（配合 `order`）。 |
| `draft` | boolean | 可选，默认 `false`。设为 `true` 时生产构建会隐藏该页，预览可见。 |
| `order` | number | 可选。手动排序权重，**越大越靠前**；未设置则按 `published` 降序。 |
| `description` | string | 可选。卡片简介 + 详情页描述。 |
| `image` | string | 可选。封面图。支持完整 URL、公共根路径（`/images/xxx.png`）、相对路径（相对本文件目录，如 `images/xxx.png`）。留空则不显示封面。 |
| `tags` | string[] | 可选。标签，列表页与详情页显示为 `#标签`。 |
| `link` | array | 可选。外链按钮数组：`{ label, icon, value }`。`icon` 可用 astro-icon 名（如 `fa7-brands:github`）、图片 URL，或留空用 `label` 首字母。 |
| `status` | string | 可选。项目状态，用标准 key（见下表）。 |
| `lang` | string | 可选。页面语言，如 `zh_CN`。 |

### 完整示例

````yaml
---
title: "Firefly"
slug: firefly
published: 2025-10-01
draft: false
order: 100
description: "一个功能丰富的开源博客主题。"
# image: "images/firefly.avif"
status: "published"
tags:
  - Astro
  - Svelte
link:
  - label: "GitHub"
    icon: "fa7-brands:github"
    value: "https://github.com/CuteLeaf/Firefly"
  - label: "文档"
    icon: "material-symbols:menu-book"
    value: "https://docs-firefly.cuteleaf.cn"
lang: ""
---
````

## 状态键值（status）

`status` 使用**标准 key**，前台会按站点语言显示本地化文案，并按状态自动配色 + 图标：

| key | 含义 | 本地化示例 |
|---|---|---|
| `planning` | 计划中 | 计划中 / Planning |
| `developing` | 开发中 | 开发中 / In Development |
| `published` | 已发布 | 已发布 / Published |
| `archived` | 已归档 | 已归档 / Archived |

- 只写标准 key 即可：`status: "published"`。
- 未知或自定义字符串会原样显示（中性灰），且不参与列表页的状态筛选。

> 列表页顶部支持**按状态筛选**（全部 / 各状态），并可按名称、描述、标签**搜索**项目。 -->
## 整体架构

采用B/S（Browser/Server）架构，前后端彻底分离。

- 前端（表现层）：Vue3（Composition API） + Vite + Pinia（状态管理） + Axios（HTTP请求） + Tailwind CSS。
- 后端（业务逻辑层）：Python 3.10 + FastAPI（异步框架） + Uvicorn（ASGI服务器） + Pydantic。
- 外部服务层：
  - AI核心：DeepSeek官方API（HTTP 或 OpenAI SDK）。
  - 联网信息源：博查（Bocha）Search API。
- 数据持久层：SQLite3。

## 三、前端界面设计

系统整体UI布局为经典的“左侧边栏 + 右侧猪对话区”。

1. 全局导航与搜索区（左侧边栏顶部）

- 品牌logo：展示DeepSeek标志。
- 快捷操作：搜索图标（触发对话搜索）、应用切换/设置图标。
- 新对话入口：鲜艳的“开启新对话”按钮，点击重置当前上下文。
- 全局搜索输入框：点击图标后展开输入框，支持在全局理事会话中按关键字检索历史问答。

2. 历史会话管理区（左侧边栏主体）

- 时间分组展示：按`今天`、`昨天`、`更早`等维度自动分组。
- 会话列表项：展示每个会话标题（默认提取第一句用户提问，支持后端自动更新），点击后主界面切换加载该会话。
- 鼠标悬停操作：悬停在列表项时，显示删除或重命名按钮。

3. 主对话框（右侧主体）

- 消息列表渲染区：交替渲染用户提问和AI回复气泡。支持Markdown渲染、代码块语法高亮、LaTex数学公式及Mermaid流程图。
- 用户输入框区（底部）：多行自适应Textarea，支持`Enter`发送，`Shift+Enter`换行。
- 控制开关：位于输入框附近，包含"深度思考"和"智能搜索"两个独立按钮，状态保存在Pinia中实时生效。
- 发送/停止按钮：输入状态下为发送按钮，流式生成状态下为停止生成按钮。

4. 搜索弹框/结果展示区（覆盖层）

- 搜索内容预览：展示命中的对话内容片段，并高亮匹配的关键词。
- 源信息：展示该条消息所属的会话标题、发生时间、发送者身份（用户/AI）。
- 跳转功能：点击结果，关闭搜索弹框，自动跳转至对应的历史会话，并精确定位高亮该条信息。

## 数据库与数据结构设计

考虑到持久化和搜索需求，后端数据库设计如下：

1. 会话表（chat_sessions）

|字段名|数据类型|说明|
|----|----|----|
|id|UUID(PK)|会话唯一主键|
|user_id|VARCHAR|用户唯一标识|
|title|VARCHAR(255)|会话标题|
|created_at|TIMESTAMP|创建时间|
|updated_at|TIMESTAMP|最后一条消息更新时间(用于排序)|

2. 消息表（chat_messages）- 核心表格

|字段名|数据类型|说明|
|----|----|----|
|id|UUID(PK)|消息唯一主键|
|session_id|UUID(FK)|所属会话ID|
|role|VARCHAR(20)|user或assistant|
|reasoning_content|TEXT|消息正文(用于搜索的重点字段)|
|created_at|TIMESTAMP|消息发生时间|

**搜索性能优化说明**：对于chat_messages表，必须在content字段上建立**全文检索索引**（如PostgreSQL的GIN索引配合pg_trgm插件，或MySQL的全文索引）。这能保证大规模历史数据下搜索接口的速度。

# 五、后端（FastAPI）核心接口设计

？？？？

# 六、检索（搜索）

## 一、核心原理对比

全文检索是”精准匹配关键词“，向量检索是”理解意图找语义“。

**最佳实践：结合全文检索（快速筛选）和向量检索（语义排序）提供更优质的搜索体验**

这里的AI搜索用的是全文检索。

## 搜索引擎工具

[博查AI 开放平台](https://open.bochaai.com/)

1. 创建API key

首次注册有免费额度，后期需要充值使用。

--？？？

1. 通信协议

SSE(Server-Sent Events)：用于流式传输大模型生成的文字，实现打字机效果。

**一句话概括**

SSE就像”收音机广播“：你（客户端）打开收音机（发起请求），电台（服务器）就会一直给你播放节目（推送数据），你不用每次都打电话去问”现在播什么“了。

- **SSE是怎么工作的？**

1. 客户端发一个普通HTTP请求，但告诉服务器：”我要长连接，你别断开“。
2. 服务器不返回完整响应，而是保持连接打开，并持续发送数据。
3. 数据格式简单，就是一段段`data: xxx \n\n`这样的文本。
4. 客户端（浏览器）收到后，通过`EventSource` API就能轻松处理这些”推送“过来的消息。

- **SSE有什么特点？**

|特点|说明|
|----|----|
|单向|只能服务器→客户端，客户端不能通过这个连接发数据回去|
|基于HTTP|不需要额外协议，通过Web服务器就能支持|
|自动连接|连接断了，浏览器会自动重新连接|
|文本格式|传输的是文本（通常是JSON字符串），不支持二进制数据|
|轻量简单|比WebSocket简单的多，不用握手升级协议|

- **适合什么场景？**

  - 实时通知（新消息提醒、系统警告）
  - 股票行情、体育比分更新
  - 新闻滚动、博客评论实时显示
  - AI对话的流式输出（像ChatGPT打字机效果）
  - 日志实时查看

- **RESTful API**：用于会话管理、历史记录获取、消息搜索等非流式操作。


申请Deepseek API key[https://platform.deepseek.com/api_keys](https://platform.deepseek.com/api_keys)


相关文档视频：https://www.bilibili.com/video/BV1wDJy61Ec6/?spm_id_from=333.788.videopod.episodes&vd_source=0e3379028aadee709d35030c4d361bef&p=84 

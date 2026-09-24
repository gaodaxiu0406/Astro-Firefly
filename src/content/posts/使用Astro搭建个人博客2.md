---
# 必填。项目名称。
title: "使用Astro搭建个人博客2"
# 可选，和文章一样使用。
slug: 使用Astro搭建个人博客遇到的问题
# 必填。发布/更新日期，如 2025-10-01。用于排序（配合 order）。
published: 2026-09-25
# 可选，默认 false。设为 true 时生产构建会隐藏该页，预览可见。
draft: true
# 可选。手动排序权重，越大越靠前；未设置则按 published 降序。
order: 1
# 可选。卡片简介 + 详情页描述。
description: "使用Astro搭建个人博客遇到的问题"
# 可选。封面图。支持完整 URL、公共根路径（/images/xxx.png）、相对路径（相对本文件目录，如 images/xxx.png）。留空则不显示封面。
# image: "./images/MongoDB安装目录.png"
# 可选。项目状态，用标准 key:planning计划中 developing开发中 published已发布 archived已归档
status: "archived"
# 分类
category: Astro
tags:
  - Astro
  - 博客
# 可选。外链按钮数组：{ label, icon, value }。icon 可用 astro-icon 名（如 fa7-brands:github）、图片 URL，或留空用 label 首字母。
# link: []
# 可选。页面语言，如 zh_CN。
# lang: zh_CN
# 可选。标签，列表页与详情页显示为 #标签。
---

## Mac 显示隐藏文件的快捷键

Mac 显示隐藏文件的快捷键是 ‌Command + Shift + .（点号）‌。在访达窗口中按下此组合，隐藏文件会显示，再按一次恢复隐藏 

# 报错

## 1. `报错request to https://registry.npm.taobao.org/pnpm failed, reason: certificate has expired`

根因：旧版淘宝镜像域名 registry.npm.taobao.org 的 SSL 证书已过期，需切换至新域名 registry.npmmirror.com。
执行以下命令切换 pnpm 镜像源并清理缓存：

```js
pnpm config set registry https://registry.npmmirror.com
pnpm store prune
```

若项目中已存在 node_modules 或锁文件，建议删除后重新安装以避免注册表不匹配错误：

```js
rm -rf node_modules pnpm-lock.yaml
pnpm install
```

## 2. 安装nvm报`Ignore insecure directories and continue [y] or abort compinit [n]`

这是 ‌zsh 提示检测到了“不安全”的补全目录‌，一般出现在装完 Homebrew、nvm 这类工具后，不是系统出大问题，但建议别直接按 y 忽略，顺手修一下权限更省心。

1）先定位问题

运行 `compaudit`，它会列出具体是哪些目录或文件权限有问题：
一般会看到类似 /usr/local/share/zsh/site-functions 或 /opt/homebrew/share/zsh 这样的路径。

2）修复权限

根据上面列出的路径，把权限改成 755（所有者可写，其他人只读）：

```js
sudo chmod -R 755 /usr/local/share/zsh/site-functions
sudo chmod -R 755 /usr/local/share/zsh
```

如果是 Apple Silicon Mac，路径可能是：

```js
sudo chmod -R 755 /opt/homebrew/share/zsh/site-functions
sudo chmod -R 755 /opt/homebrew/share/zsh
```

改完再执行 `source ~/.zshrc` 或重开终端，提示应该就没了。

3）如果还不行

说明是所有者不对，可以顺带把属主也改掉：

```js
sudo chown -R root:staff /usr/local/share/zsh
```

> 不建议用 ZSH_DISABLE_COMPFIX=true 直接跳过检查，这等于关掉了 zsh 的安全防线，补全脚本有被篡改的风险。

## 3. mac运行`pnpm env ls`报错 `ERR_PNPM_ENV_NO_NODE_DIRECTORY  Couldn't find Node.js directory in /Users/xiu/Library/pnpm/nodejs`

这个报错的意思是 `pnpm` 在 `/Users/xiu/Library/pnpm/nodejs` 这个目录下没有找到 `Node.js` 的安装目录。这通常是因为用 `pnpm env` 管理 `Node` 版本时，之前安装的版本被删除或移动了，导致 `pnpm` 记录的路径失效。

可以试试先重新安装一个 `Node` 版本，把目录重建起来：‌
1）‌安装一个 LTS 版本‌：运行 `pnpm env use --global lts`，这会自动下载并安装 `Node.js` 到 `pnpm` 管理的目录中。
2）‌查看当前状态‌：安装完成后，再运行 `pnpm env ls` 检查是否能正常列出已安装的版本。
3）‌如果安装失败或目录仍然为空‌：可以手动检查一下 `/Users/xiu/Library/pnpm/nodejs` 这个路径是否存在，以及里面有没有内容。如果目录不存在，可以手动创建：`mkdir -p ~/Library/pnpm/nodejs`，然后再试一次上面的安装命令。

> 如果之前是通过 `pnpm env` 安装过 `Node` 并且后来卸载了，重新安装一次通常就能解决这个报错。如果重装后仍然不行，可以检查一下 `pnpm` 的版本，尝试更新到最新版：`npm install -g pnpm@latest`。

## 4. 运行`npm install -g pnpm`报错`npm error code ERR_INVALID_AUTH`、`npm error Invalid auth configuration found: email must be renamed to //registry.npmmirror.com/:email in user config`

这个报错 `npm error code ERR_INVALID_AUTH` 是因为你的 `npm` 全局配置文件（`.npmrc`）中存在‌格式不规范或过时的认证配置‌。

具体来说，`npm` 检测到配置文件中有一个裸写的 `email` 字段，或者某个 `registry` 下的认证信息格式不符合当前版本的安全规范。`npm` 要求所有的 `registry` 特定配置（如`email`、`token`、`auth`）必须加上 `registry` 的前缀路径。

解决方案：

### 方案一(**亲测有效**)

使用官方脚本安装（避开 `npm` 配置问题）
如果你只是想安装 `pnpm`，且不想处理 `npm` 复杂的配置问题，可以使用 `pnpm` 官方的独立安装脚本，它不依赖 `npm` 的全局配置：

Mac/Linux:‌

```js
curl -fsSL https://get.pnpm.io/install.sh | sh -
```

‌Windows (PowerShell):‌

```js
iwr https://get.pnpm.io/install.ps1 -useb | iex
```

这种方式可以避免因 `npm` 配置错误导致的安装失败。安装完成后，记得将 `pnpm` 的安装目录添加到系统环境变量 `PATH` 中（脚本通常会提示你如何操作。

### 方案二

请按照以下步骤清理和修复你的 `npm` 配置：

1. 找到并编辑 `.npmrc` 文件。
你需要找到用户级别的 `npm` 配置文件。
‌Mac/Linux‌: 通常位于 `~/.npmrc`。
‌Windows‌: 通常位于 `C:\Users\你的用户名\.npmrc`。
你可以使用`npm config edit`命令直接打开编辑。

2. 修改错误的配置项

在打开的文件中，查找类似以下的行：

```js
// ❌ 错误写法（导致报错的原因）
email=yourname@example.com
// registry.npmmirror.com/:_authToken=xxxxx
```

将其修改为带前缀的格式，或者直接删除不必要的 `email` 字段（现代 `npm`/`pnpm` 安装通常不需要配置 `email`）：

方案 A：删除 `email`（推荐）‌——**亲测有效**
大多数情况下，安装 `pnpm` 不需要邮箱配置，直接删除 `email=...` 这一行即可。

‌方案 B：修正格式（如果必须保留）‌
如果某些私有仓库强制要求邮箱，必须加上 `registry` 前缀：

```js
// ✅ 正确写法
registry.npmmirror.com/:email=yourname@example.com
```

> 注意‌：检查文件中是否还有其他没有前缀的敏感字段（如 `_auth`, `_authToken`），确保它们都绑定在具体的 `registry URL` 下，例如`registry.npmjs.org/:_authToken=...`。

1. 清除缓存并重试

修改保存后，建议清除一下 `npm` 缓存，然后重新安装：

```js
// 清除缓存
npm cache clean --force

// 重新全局安装 pnpm
npm install -g pnpm
```

如果还是不行，运行`curl -fsSL https://get.pnpm.io/install.sh | sh -`安装pnpm。

## 5.运行`curl -fsSL https://get.pnpm.io/install.sh | sh -`输出`Done in 306ms using pnpm v12.5.1`，但运行pnpm -v还是之前的版本号

下载pnpm成功，请按照提示在终端中运行以下命令，使环境变量立即生效：

```js
source /Users/xiu/.zshrc
```

执行完毕后，你可以运行 `pnpm -v` 来验证 `pnpm` 是否已正确安装并可在当前终端中使用。

如果提示`Done in 306ms using pnpm v12.5.1`，但运行`pnpm -v`还是之前的版本号

这种情况通常是因为‌Shell（终端）缓存了旧的可执行文件路径‌，或者系统中存在‌多个 pnpm 安装实例导致路径冲突‌。虽然 pnpm setup已经更新了配置文件，但当前运行的终端会话可能仍在使用内存中缓存的旧路径。
请按照以下步骤依次排查并解决：

1. 清除 Shell 命令缓存（最可能的原因）

Zsh 和 Bash 会缓存命令的路径以提高执行速度。即使你修改了 PATH，Shell 可能仍然指向旧的 pnpm 位置。
在当前终端中运行以下命令来清除缓存：

```js
hash -r
```

(如果是 Bash，也可以尝试 rehash)
然后再次检查版本：

```js
pnpm -v
```

如果清除缓存后无效（还是显示旧版本号），需要确认当前终端到底在执行哪个 pnpm。运行：

```js
which pnpm
```

- ‌预期结果‌：应该输出 xxx/Library/pnpm/bin/pnpm（即你刚才配置的新路径）。
- ‌异常结果‌：如果输出的是其他路径（如 `/usr/local/bin/pnpm`、`~/.nvm/.../bin/pnpm` 或 `/opt/homebrew/bin/pnpm`），说明系统优先找到了旧版本的 `pnpm`。

2. 解决路径冲突

如果 `which pnpm` 指向了旧路径，你有两种选择：

方案 A**亲测有效**：删除旧版本的 `pnpm`（推荐）

如果旧版本是通过 `npm` 全局安装或 `Homebrew` 安装的，且你希望统一使用 `pnpm env` 管理的版本，可以删除旧的可执行文件。
假设 `which pnpm` 输出的是 `/usr/local/bin/pnpm`：

```js
rm /usr/local/bin/pnpm
// 如果有 pnpm.cmd 或其他相关软链接，也一并删除
```

删除后，再次运行 `hash -r` 和 `pnpm -v`，系统就会自动找到新配置路径下的 `pnpm`。**亲测有效**

方案 B：调整 PATH 优先级

如果你必须保留旧路径中的某些工具，可以手动调整 `~/.zshrc` 中的 `PATH` 顺序，确保 `$PNPM_HOME/bin` 在其他路径之前。

打开配置文件：

```js
nano ~/.zshrc
```

确保 `export PATH="$PNPM_HOME/bin:$PATH"` 这一行位于其他可能包含 `node/pnpm` 的路径设置‌之后‌（因为 `PATH` 是从左向右匹配的，前面的优先级高；或者确保它被添加到了 `PATH` 的最前面）。

```js
source ~/.zshrc
hash -r
pnpm -v
```

## 6. 运行`git clone https://github.com/gaodaxiu0406/Astro-Firefly.git`报错`error: RPC failed; curl 28 Failed to connect to github.com port 443 after 75002 ms: Couldn't connect to server`

在使用 Git 进行代码管理的过程中，经常会遇到各种各样的问题，其中之一就是在执行 git clone 或 git pull 等操作时出现 “fatal: unable to access ‘https://github.com/…/.git’: Recv failure Connection was reset” 的报错。这个问题通常是由网络连接问题或代理设置不正确导致的。

方法一：取消代理设置

这是最常见的解决方法之一，通过在终端执行以下命令，可以取消 Git 的代理设置：

```js
git config --global --unset http.proxy 
git config --global --unset https.proxy
```

这样就可以清除 Git 的代理设置，让其直接连接网络进行操作。

## 6. 运行`git push -u origin blog-dev`报错f`atal: Authentication failed for 'https://github.com/gaodaxiu0406/Astro-Firefly.git/'`

根因：GitHub 已禁用账号密码登录 HTTPS，必须使用个人访问令牌（Personal Access Token）替代密码；且本地 Git 可能缓存了旧的错误凭据。

### 6.1 清除本地缓存的旧凭据（确保下次推送时重新提示输入）

```js
// Windows/macOS/Linux 通用命令，清除 github.com 的缓存凭据
printf "protocol=https\nhost=github.com\n\n" | git credential reject
```

### 6.2 生成新的 Personal Access Token (PAT)

- 登录 GitHub，点击右上角头像 -> ‌Settings‌。
- 左侧菜单底部 -> ‌Developer settings‌ -> ‌Personal access tokens‌ -> ‌Tokens (classic)‌。
- 点击 ‌Generate new token (classic)‌。
  - ‌Note‌: 填写备注（如 git-push）。
  - Expiration‌: 选择有效期（建议 30-90 天，或 No expiration）。
  - ‌Select scopes‌: 勾选 ‌repo‌ (Full control of private repositories)。
  - 点击底部 ‌Generate token‌，‌立即复制‌生成的令牌（以 ghp_ 开头），关闭页面后无法再次查看。

### 6.3 重新推送并输入新凭据

```js
git push -u origin blog-dev
```

- Username‌: 输入你的 GitHub 用户名。
‌- Password‌: 粘贴刚才复制的 ‌Personal Access Token‌（不是登录密码。

## 7. 运行`pnpm install`报错`Error: ERR_PNPM_PNPM_ENGINE_NO_NATIVE_BINARY`

这个报错说的是：项目固定了 pnpm 11.22.0，但这个版本的预编译二进制不支持你的 Mac 的 darwin-x64 架构，所以 pnpm 拒绝运行。

最直接的解决办法是设置 pmOnFail 为 ignore，跳过版本切换‌，让 pnpm 继续用你当前已经装好的版本工作。可以这样设置：

```js
pnpm config set pmOnFail ignore
```

如果上面这条命令本身也触发版本检查，可以加 --location=project 试试：

```js
pnpm config set pmOnFail ignore --location=project
```

如果还是不行，找到项目中的`package.json`文件，将`"packageManager": "pnpm@11.22.0"`改为你安装的pnpm版本`"packageManager": "pnpm@12.5.1"` (当然，这个方法比较暴力了，最好你本地是最新的pnpm版本，或者高于原package.json中pnpm的版本，否则出问题的概率可能会增加)。

## 8. 本地`git checkout xx`切换分支后，`node`、`npm`、`pnpm`都找不到了

运行

```js
source ~/.nvm/nvm.sh
```

再运行

```js
node -v
npm -v
pnpm -v
```

就能输出相关版本号了。

## 部署遇到的相关问题

### 1. 使用cloudflare部署

问题：使用cloudflare部署访问地址https://astro-firefly.gdxiu666.workers.dev一直转圈无法访问

运行nslookup astro-firefly.gdxiu666.workers.dev输出：

```js
Server:		fe80::a646:b4ff:fe30:20b8%6
Address:	fe80::a646:b4ff:fe30:20b8%6#53
Non-authoritative answer:
Name:	astro-firefly.gdxiu666.workers.dev
Address: 74.86.118.24
```

问题找到了：`DNS` 被污染，返回的不是 `Cloudflare` 的 IP。

> 当我到知道原因是 DNS 被污染后，就没有继续了。

`74.86.118.24` 不属于 `Cloudflare` 的任何 `IP` 段。`Cloudflare` 的 `IP` 通常在 `104.16.x.x`–`104.31.x.x`、`172.64.x.x`–`172.71.x.x`、`162.158.x.x` 等范围内。

这意味着你从中国大陆访问时，`workers.dev` 域名的 `DNS` 解析被 `GFW` 污染，返回了一个假 `IP`，连接到该 `IP` 后自然一直挂起（转圈）。这也解释了为什么 `GraphQL` 分析显示零请求——请求根本没有到达 `Cloudflare`。

#### 解决方案

#### 方案 1：绑定自定义域名（推荐）

如果你有自己的域名（如 `gdxiu666.com`），可以将其添加到 `Cloudflare` 并配置为 `Worker` 的自定义域名。自定义域名走 Cloudflare 的代理 IP，通常不受 `workers.dev` 污染影响。

#### 方案 2：使用代理 `/VPN` 访问

通过 `VPN` 或代理访问 `workers.dev` URL，绕过 `DNS` 污染。

#### 方案 3：修改本地 `DNS`

将本机 `DNS` 改为 `1.1.1.1` 或 `8.8.8.8`，但这在中国大陆可能仍然被污染。

### 2. 使用netlify部署

### 2.1 运行`git push origin dev`报错`fatal: unable to access 'https://github.com/gaodaxiu0406/Astro-Firefly.git/': Error in the HTTP2 framing layer`

这个报错是非常典型的Git访问GitHub的443端口连接超时问题，结合你当前使用的Firefly Astro博客项目场景，你可以按照从易到难的优先级依次尝试以下排查方案，快速解决问题：

重新运行`git push origin dev`依然报错

测试`GitHub`的443端口是否可以正常连通：
在终端执行命令测试：`nc -zv github.com 443`，`Windows`用户可以在开启`Telnet`功能后执行`telnet github.com 443`。如果连接失败，说明当前网络的`HTTPS`流量被防火墙、`ISP`或者安全软件拦截。

可以尝试用curl快速验证GitHub的HTTPS连通性：

```js
curl -I https://github.com -m 10
```

排查`DNS`解析故障：执行`nslookup github.com`，如果返回的`IP`地址明显异常，说明是`DNS`解析到了错误的失效节点，可以更换公共`DNS`服务，刷新本地`DNS`缓存后重试。

### 2.2 部署成功后，通过本地运行代码`git push origin dev`，成功将代码推送到github的dev分支，但部署后的页面未更新，打开netlify控制台报错

图片？？？





？？？

## 怎么用 pnpm 自带功能切换

- ‌全局切换‌：使用命令 `pnpm env use --global <version>`，如 `pnpm env use --global 18`。
- ‌查看版本‌：执行 `pnpm env ls` 可列出已安装的 `Node` 版本。
- ‌清理旧版‌：使用 `pnpm env remove <version>` 卸载不再需要的 `Node` 版本。
- ‌修复 `pnpm` 失效‌：切换 `Node` 版本后，`pnpm` 可能报“不是内部或外部命令”，需在新版本下重新全局安装 `pnpm`（`npm install -g pnpm`。
- 缓存隔离‌：可通过配置 `PNPM_HOME` 环境变量，让不同 `Node` 版本使用独立的 `pnpm` 全局工具目录，避免冲突。

> 怎么让项目自动切换版本

- ‌锁定版本‌：在项目根目录创建 `.npmrc` 文件，添加 `use-node-version=18.17.0`。
- ‌自动生效‌：配置后，在该目录下运行 `pnpm` 令时会自动切换到指定 `Node` 版本，无需手动干预。
- ‌兼容检查‌：建议配合 `package.json` 中的 `engines` 字段，强制检查 `Node` 版本是否符合项目要求。‌‌‌

## git常用命令

```js
```
astro-firefly-blog
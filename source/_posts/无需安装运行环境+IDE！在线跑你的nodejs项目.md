---
title: 无需安装运行环境+IDE！在线跑你的nodejs项目
author: zfrg
tags:
  - Web
categories:
  - 开发
excerpt: <p>StackBlitz 基础用法入门</p>
date: 2026-03-06 22:07:23
---
## 核心出装

### StackBlitz WebContainers

> [StackBlitz](https://stackblitz.com/ "StackBlitz | Instant Dev Environments | Click. Code. Done.") 是 JavaScript 生态系统中一款即时的全栈 Web 集成开发环境（IDE）。它由 WebContainers 提供支持，这是首个基于 WebAssembly 的操作系统，可在毫秒内安全地在您的浏览器标签页中启动 Node.js 环境。
> 现在，你可以利用网络来构建网络。

大概意思就是借助 wa 技术，在你的浏览器跑了个 OS 且内置 Node.js 等开发环境。在你的浏览器中它表现为一个近似 VSCode 的 Web IDE。与 [vscode.dev](https://vscode.dev/ "vscode for web") 不同，你能在此处使用终端功能，运行项目。不但如此，它也不同于 [CodeStudio](https://codestudio.net "Tencent CodeStudio")，由于项目实际运行于你的本地浏览器，你无需担心服务器距离过远，使用时间限制等传统云端 IDE 的问题。

**StackBlitz 具有以下主要特点**：

- 无与伦比的安全性：所有开发都在您的浏览器标签页中进行，包括运行 Node.js 和 git

- 速度惊人：整个开发环境在毫秒内即可搭建完成——甚至重新安装`node_modules`也像刷新页面一样简单

- 无论在线还是离线都能工作：即使中途失去网络连接，也能继续工作

- 您的应用始终在线：您的应用永不休眠，且没有带宽限制——您可以随意与朋友、同事和社区分享该URL！

- 使用Chrome开发者工具，前后端应用均可实现无缝调试！

你可以直接从 StackBlitz Dashboard 创建一个项目，自选框架，无需 git 储存库。

如果你希望从 [Github](https://github.com/ "GitHub · Change is constant. GitHub keeps you ahead. · GitHub") 平台导入，使用以下格式的 URL 即可迅速导入。

**一般导入**：

```url
stackblitz.com/github/{gh_username}/{repository_name}
```

**复刻项目**：

```url
stackblitz.com/fork/github/{gh_username}/{repository_name}
```

**特定分支、标签、提交**：

```url
stackblitz.com/github/{GH_USERNAME}/{REPOSITORY_NAME}/tree/{TAG|BRANCH|COMMIT}
```

**更多自定义参数**：

```url
stackblitz.com/fork/github/{gh_username}/{repository_name}?startScript={npm_script_name}&title={custom title}
```

若需使用 `git` 命令操作你的储存库等与平台高度绑定的操作请看下文。

### CodeFlow IDE

> Codeflow可一键集成GitHub，实现无缝编码工作流程。

相较于 Classic Editor（上文所指），CodeFlow 的界面更接近于 Visual Studio Code 的同时增加了更多 git 操作所需的功能使你可以在 CodeFlow 中拉取请求、提交更改、推送代码。

你仍可以通过一定格式的 URL 快速地启动 CodeFlow 并导入储存库，格式如下：

```url
pr.new/{gh_username}/{repository_name}
```

如果你正在访问一个 Github 储存库，在`github.com`前面加上`pr.new/`也可快速转到 CodeFlow IDE。

```url
pr.new/github.com/{gh_username}/{repository_name}
```

### 举个栗子

以 [gamemcu](https://github.com/gamemcu) 大佬的 [www-genshin](https://github.com/gamemcu/www-genshin) 项目为例，在 CodeFlow 中打开，得到的 URL 如下：

```url
pr.new/gamemcu/www-genshin
```

[![Open in Codeflow](https://developer.stackblitz.com/img/open_in_codeflow.svg)](https:///pr.new/gamemcu/www-genshin)

通过 StackBlitz 你可以在任何一处使用现代浏览器运行全栈项目！

---
title: 在最新的Win10系统中复活 Internet Explorer
author: zfrg
tags:
  - Windows
  - 浏览器
categories:
  - 开发
excerpt: >-
  <p>Internet Explorer（简称IE），作为无数国人的童年回忆，现在已经被微软“砍掉”了。在 Windows 10 22H2
  中，你仍能从开始菜单里找到 IE 的快捷方式。但很遗憾，你无法从中正确启动 IE，而是打开了 Microsoft Edge
  的新窗口。本文将教你优雅地将IE复活。</p>
date: 2026-01-02 05:03:57
---
## 情景引入

Internet Explorer（简称IE），作为无数国人的童年回忆，现在已经被微软“砍掉”了。在 Windows 10 22H2 中，你仍能从开始菜单里找到 IE 的快捷方式。但很遗憾，你无法从中正确启动 IE，而是打开了 Microsoft Edge 的新窗口。

打开这个快捷方式目标的所在路径`C:\Program Files (x86)\Internet Explorer`，是完整的 Internet Explorer。这说明，微软（大概）为了强大的兼容性，在系统中保留了 IE 的内核。

如果我们想要使用 IE 访问一些比较老的网站时，应该如何重新启用呢？

## 方法介绍

### 原理

既然常规方法不行，那就只能使些“歪门邪道”了。

众所周知，`mshta`调用的内核正是 IE 的。那我们有没有可能借助`mshta`打开一个 IE 内核的浏览器窗口，然后再新建一个正常的完整的 IE 浏览器窗口，最后关闭`mshta`的窗口实现复活 IE 呢？

### 实现

实践出真知。要完成打开新窗口关闭自身窗口等操作可以借助`JavaScript`完成。

```js
window.open();
window.close();
```

最后让`mshta`执行这段js脚本就行了

```batch
mshta.exe javascript:window.open();window.close();
```

创建快捷方式执行这段命令，IE 浏览器窗口如期显示。

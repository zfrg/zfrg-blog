---
title: 给Photopea标题栏左上角加上个图标
author: zfrg
tags:
  - 浏览器
  - 用户脚本
categories:
  - 开发
excerpt: >-
  <p>Photopea 是一款功能强大的在线图像编辑工具，支持以
  PWA（渐进式网页应用）形式安装到本地设备使用。然而，在实际使用过程中，部分用户可能会遇到界面显示不完整、标题栏高度不适配等问题，影响操作体验。为了解决这一问题，我编写了一个轻量级的
  Tampermonkey 用户脚本。</p>
date: 2026-01-01 18:20:32
---
## 背景介绍

Photopea 是一款功能强大的在线图像编辑工具，支持以 PWA（渐进式网页应用）形式安装到本地设备使用。然而，在实际使用过程中，部分用户可能会遇到界面显示不完整、标题栏高度不适配等问题，影响操作体验。

为了解决这一问题，我编写了一个轻量级的 Tampermonkey 用户脚本。该脚本旨在提升Photopea在PWA模式下的视觉一致性和交互体验。

## 脚本内容

### 脚本功能亮点

* 添加官方图标至标题栏：自动在Photopea顶部栏插入官方缩略图标，提升视觉识别度和界面美观性。
* 修复标题栏高度异常：检测并修正某些情况下标题栏高度从31px变为32px的问题，确保UI稳定显示。
* 禁用右键菜单干扰：屏蔽页面默认右键菜单行为，防止误触或干扰用户自定义快捷操作。
* 自动适配加载时机：通过监听DOM变化，确保脚本在页面结构加载完成之后正确执行。

### 技术实现简述

脚本基于原生 JavaScript 编写，利用了以下关键技术点：

* 使用 `MutationObserver` 监听DOM节点变化，动态注入图标元素；
* 通过 `setInterval` 定时检查并修正特定元素的高度样式；
* 禁止全局右键菜单行为，提升用户体验一致性；
* 图标资源引用自Photopea官网，保持视觉统一。

### 使用说明

1. 安装 [Tampermonkey](https://www.tampermonkey.net/) 浏览器扩展；
2. 新建一个用户脚本，并粘贴本脚本内容；
3. 访问 [Photopea官网](https://www.photopea.com/) 并以PWA模式运行；
4. 观察标题栏是否成功显示图标，同时无高度跳动问题。

> 注意：此脚本仅适用于 Photopea 官方网站，且需在桌面端浏览器中配合Tampermonkey使用效果最佳。

效果图：

![](https://livefile.xesimg.com/programme/python_assets/79ac1584d47764af590d574a0839916c.webp)

### 脚本代码

```js
// ==UserScript==
// @name         Photopea窗口图标&标题栏宽度优化
// @namespace    http://zfrg-blog.de5.net/
// @version      2025-12-27
// @description  优化PhotopeaPWA使用体验
// @author       zfrg
// @match        https://www.photopea.com/*
// @icon         https://www.photopea.com/promo/thumb256.png
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    // Your code here...
    document.body.oncontextmenu = function() {return false;};
    // GM_addStyle(".app > div > div:nth-child(3) {height: 32px !important ; }");

    setInterval(function() {
        var targetElement = document.querySelector('.app > div > div:nth-child(3)');

        if (targetElement && targetElement.style.height === '31px') {
            targetElement.style.height = '32px';
        }
    }, 0);

    var observer = new MutationObserver(function(mutationsList) {
        var count = 0;

        for (var mutation of mutationsList) {
            if (mutation.type === 'childList' && mutation.addedNodes.length > 0) {
                var topbar = document.querySelector('.topbar');
                if (topbar) {
                    count++;

                    if (count === 1) {
                        var c = document.createElement('span');
                        var icon = document.createElement('img');
                        icon.src = "https://www.photopea.com/promo/thumb256.png";
                        icon.style = "width: 18px;height: 18px;position: relative;left: 5px;top: 4px;bottom: 4px;padding-right: 10px;user-select: none;-webkit-user-select: none;-webkit-user-drag: none;app-region: no-drag;";
                        icon.oncontextmenu = function() {
                            return false;
                        };
                        c.appendChild(icon);
                        topbar.insertBefore(c, topbar.firstChild);
                        observer.disconnect();
                    }
                }
            }
        }
    });

    observer.observe(document.documentElement, { childList: true, subtree: true });

})();
```

### 总结

该脚本虽小，但在改善Photopea PWA使用体验方面起到了重要作用。它不仅提升了UI的一致性，还通过细节调整增强了整体可用性。未来可考虑进一步扩展为功能插件包，提供更多个性化配置选项。

---
title: Quartz 在新选项卡中打开外部链接
date: 2024-11-29T14:12
tags:
  - Quartz
---

Quartz 中的`a`标签默认没有`target=_blank`属性，虽然这是正确的，但是对于外部连接，我还是习惯在新标签页中打开。

这个 PR 中提到了此问题: https://github.com/jackyzha0/quartz/pull/127

按照[@nickian](https://github.com/jackyzha0/quartz/pull/127#issuecomment-2054171439)提供的方法，可通过自定义 js 的方式实现新标签页打开链接。

编辑  `quartz/components/Head.tsx`. 在  `<head>`  标签中引用自定义 js 文件:

`<script src="/static/custom.js" defer></script>`

新建 js 文件  `static/custom.js` :

```javascript
document.addEventListener('DOMContentLoaded', function() {
  document.addEventListener('click', function(event) {
    if (event.target.matches('a.external')) {
      event.preventDefault();
      window.open(event.target.href, '_blank');
    }
  });
});
```

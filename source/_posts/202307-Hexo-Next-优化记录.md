---
title: Hexo-Next 优化记录（持续更新中...）
description: 科研不搞，文章不写，还搁这持续优化呢？？？
categories:
tags:
sticky: 0
---

仅对[官方手册](https://theme-next.js.org/)中没有的，或出错的作一些补充。

## 使用 wps 网盘进行 pdf 文件分享-230720

因为发现 github 的仓库容量有[大小限制](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github?platform=windows)，所以 pdf 文档（教材之类）应该都不会放在博客一起了，另外存在其它网盘。而之前充了好几年的 wps 会员，所以会使用 wps 网盘（应该也算是比较便宜的吧？不太了解，以后到期可能会换其它网盘）进行文件分享。

[测试](https://kdocs.cn/l/cgRgDDUkVbqd)

还是比较方便。

## 对站点内部 page 的链接引用-230718

可以在[github 仓库](https://github.com/dc-deng/dc-deng.github.io/tree/main)里直接点开路径，复制。只需要到文件夹名就行，不用到`index.html`。比如，引用[这篇](/2023/07/17/Hexo-Next-优化记录)，链接是：`/2023/07/17/Hexo-Next-优化记录`。

{% note warning %}
路径前一定得以`/`开头，表示从根目录`https://github.com/dc-deng`开始。`../`表示从上级目录开始，`~/`是无效的，开头什么都不加，则表示从当前目录开始。
{% endnote %}

## 添加 pdf-230717

这里将会是一个 pdf：{% pdf /latex-notes/Notes-on-classical-electrodynamics/Notes-on-classical-electrodynamics.pdf %}

- `latex-notes`文件夹放在`/source`里，加了个`index.md`，相当于是一个“隐藏的页面”。
- 插入格式类似于：`{% pdf /latex-notes/Notes-on-classical-electrodynamics/Notes-on-classical-electrodynamics.pdf %}`
  {% note warning %}
  路径不能出现中文！！！
  {% endnote %}
- 右键即可保存 pdf。

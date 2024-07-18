---
title: Hexo-Next 优化记录（持续更新中...）
description: 仅对官方手册（https://theme-next.js.org/）中没有的，或出错的作一些补充。
categories:
tags: [hexo-next]
sticky: 0
---

# 对站点内部 page 的链接引用-230718

可以在[github 仓库](https://github.com/dc-deng/dc-deng.github.io/tree/main)里直接点开路径，复制。只需要到文件夹名就行，不用到`index.html`。比如，引用[这篇](/2023/07/17/Hexo-Next-优化记录)，链接是：`/2023/07/17/Hexo-Next-优化记录`。

{% note warning %}
路径前一定得以`/`开头，表示从根目录`https://github.com/dc-deng`开始。`../`表示从上级目录开始，`~/`是无效的，开头什么都不加，则表示从当前目录开始。
{% endnote %}

# 添加 pdf-230717

这里将会是一个 pdf：{% pdf /latex-notes/Notes-on-classical-electrodynamics/Notes-on-classical-electrodynamics.pdf %}

- `latex-notes`文件夹放在`/source`里，加了个`index.md`，相当于是一个“隐藏的页面”。
- 插入格式类似于：`{% pdf /latex-notes/Notes-on-classical-electrodynamics/Notes-on-classical-electrodynamics.pdf %}`
  {% note warning %}
  路径不能出现中文！！！
  {% endnote %}
- 右键即可保存 pdf。

# 使用 wps 网盘进行 pdf 文件分享-230720

因为发现 github 的仓库容量有[大小限制](https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github?platform=windows)，所以 pdf 文档（教材之类）应该都不会放在博客一起了，另外存在其它网盘。而之前充了好几年的 wps 会员，所以会使用 wps 网盘来分享文件。

链接[测试](https://kdocs.cn/l/cgRgDDUkVbqd)

pdf 插入测试：

{% pdf https://kdocs.cn/l/cgRgDDUkVbqd %}

只要把`{% pdf <url> %}`中的`<url>`换成网盘链接即可。

> 是直接插入了金山文档的 UI，看起来效果更优。

# 多台电脑同步更新博客

- 教程见：[Hexo 在多台电脑上提交和更新](https://blog.csdn.net/K1052176873/article/details/122879462?csdn_share_tail=%7B%22type%22%3A%22blog%22%2C%22rType%22%3A%22article%22%2C%22rId%22%3A%22122879462%22%2C%22source%22%3A%22unlogin%22%7D)。
- 防丢失，网页保存如下：
  {% pdf https://kdocs.cn/l/coz0xdvm2E72 %}

# 数学公式测试

- 行内公式：$f(x)=\frac{a+1}{b\sqrt{x^2+y^2}}\cdot\cos(\omega t + kx)\exp{\left\{i(\omega t + kr)\frac{\omega}{k}\right\}}$
- 行间公式：
  $$
  \begin{equation}
    f(x)=\frac{a+1}{b\sqrt{x^2+y^2}}\cdot\cos(\omega t + kx)\exp{\left\{i(\omega t + kr)\frac{\omega}{k}\right\}}
  \end{equation}
  $$

# 修改博客字体-240717

中文字体为 [LXGW WenKai/霞鹜文楷](https://github.com/lxgw/LxgwWenKai)，英文字体为 Windows 自带的 Cambria Math，可以同时支持英文和公式字体。两个都为衬线字体，但是粗细过渡都很平滑，看起来挺搭。我 LaTeX 的公式字体也是 Cambria Math，这款字体看着确实挺舒服的。

下面是一些设置字体里踩过的坑：

- 按照 [Next 官方文档](https://theme-next.js.org/docs/theme-settings/miscellaneous#Fonts-Customization)说的，改字体只要在 \_config.next.yml 文件里的 font 一栏里改就行，但是我加上两套字体希望分别设置中英文字体却老是失败：
  ```
  global:
    external: false
    # family: Source Han Serif CN # 思源宋体
    # family: Source Han Sans CN VF # 思源黑体
    family: Cambria Math, LXGW WenKai # 英文：Cambria Math，中文：霞鹜文楷
    # family: MiSans
    size: 0.95
  ```
  最后只能在 ~\\themes\\next\\source\\css_variables 里的 base.styl 文件里直接改字体：
  ```
  // Font families.
  $font-family-chinese      = "Cambria Math", "LXGW WenKai", "Microsoft YaHei";
  ```
- 除了字体以外，还改了字体颜色（base.styl）
  ```
  // Global text color on <body>
  $text-color                   = $black-dim; // origin: black-light
  $text-color-dark              = $black-light; // origin: grey-light; for dark mode?
  ```
  和字体大小（\_config.next.yml，如上）。
- 另外记录一下命令行中打印出英文字族名称的代码（from chatGPT）:
  ```shell
  Add-Type -AssemblyName System.Drawing
  $fonts = New-Object System.Drawing.Text.InstalledFontCollection
  $fonts.Families | Where-Object { $_.Name -notmatch "[\u4e00-\u9fa5]" } | ForEach-Object {
      [PSCustomObject]@{
          FontFamily = $_.Name
      }
  } | Format-Table -AutoSize
  ```

# 修改博客标题和链接颜色；开启阅读进度等-240718

- 修改标题颜色（base.styl）：
  ```
  $WildStrawberry         = #ED2367; // for title
  $CornflowerBlue         = #6395ED; // for headline
  ```
  这两个颜色是 latex 的 xolor 包里的颜色，用 PPT 提取的，也分别是我 latex 模板里大标题和文内标题的颜色。但是博客里的 headline 的颜色我暂时不知道怎么改。
  ```
  $subtitle-color                 = $WildStrawberry;
  $site-subtitle-color            = $WildStrawberry;
  ```
- 修改链接颜色（ ~\\themes\\next\\source\\css\\\_common\\components\\post\\post.styl ）：
  ```
  .post-body p a{
    color: #ED2367; // WildStrawberry
    border-bottom: none;
    &:hover {
      color: #B50F46; // Darker. Choosed with the help of powerpoint.
      text-decoration: underline;
    }
  }
  ```
- 开启阅读进度（\_config.next.yml）：
  ```
  # Reading progress bar
  reading_progress:
    enable: true # false
    # Available values: top | bottom
    position: top
    color: "#37c6c0"
    height: 3px
  ```
- 目录配置（\_config.next.yml）：
  ```
  # Table of Contents in the Sidebar
  # Front-matter variable (unsupport wrap expand_all).
  toc:
    enable: true
    # Automatically add list number to toc.
    number: true
    # If true, all words will placed on next lines if header width longer then sidebar width.
    wrap: true # false
    # If true, all level of TOC in a post will be displayed, rather than the activated part of it.
    expand_all: true
    # Maximum heading depth of generated toc.
    max_depth: 6
  ```
- 侧边栏配置（\_config.next.yml）：

  ```
  sidebar:
    # Sidebar Position.
    position: left
    #position: right

    # Manual define the sidebar width. If commented, will be default for:
    # Muse | Mist: 320
    # Pisces | Gemini: 240
    #width: 300
    width: 370

    # Sidebar Display (only for Muse | Mist), available values:
    #  - post    expand on posts automatically. Default.
    #  - always  expand for all pages automatically.
    #  - hide    expand only when click on the sidebar toggle icon.
    #  - remove  totally remove sidebar including sidebar toggle.
    display: post

    # Sidebar padding in pixels.
    padding: 18
    # Sidebar offset from top menubar in pixels (only for Pisces | Gemini).
    offset: 12
    # Enable sidebar on narrow view (only for Muse | Mist).
    onmobile: true # false
  ```

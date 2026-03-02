---
title: Zensical 中文教程
hide:
#   - navigation
#   - toc 
  - footer
comments: false
---

<center><font class="custom-font ml3">最好的 Zensical教程</font></center>

<style>
.custom-font {
    font-size: 31px;
    color: #757575;
}
@media (max-width: 768px) {
    .custom-font {
        font-size: 25px;
    }
}
</style>


<style>
.custom-font {
    font-size: 31px;
    color: #757575;
}
@media (max-width: 768px) {
    .custom-font {
        font-size: 25px;
    }
}
</style>


<div class="grid cards" markdown>

-   :material-rocket-launch:{ .lg .middle } __为什么选择 Zensical？__

    ---
    
    ![Zensical Logo](https://zensical.org/assets/zensical.svg){ class="responsive-image" align=right width="200" style="border-radius: 15px;" }
    
    - [x] [MkDocs for Material](https://squidfunk.github.io/mkdocs-material/blog/2025/11/11/insiders-now-free-for-everyone/) 已停止更新进入维护模式，[Zensical](https://zensical.org/) 是官方推荐的新一代博客系统
    - [x] 即时导航，无需刷新页面
    - [x] 无需费心，开箱即用
    - [x] 性能优异，加载迅速
    
    === "Mac/PC 端"
        请在上方标签选择分类 / 左侧目录选择文章
    
    === "移动端"
        请点击左上角图标选择分类和文章

</div>
<style>
@media (max-width: 768px) {
    .responsive-image { display: none; }
}
</style>

> 不同于市面上过时的 [MkDocs 教程](https://wcowin.work/Mkdocs-Wcowin/)（其实也是我写的），本站提供了 **最详细、最便捷、最前沿** 的 Zensical 中文教程，与 [官方发布](https://zensical.org/docs/get-started/) 的版本同步。包含了 Zensical 的安装、配置、主题美化、博客系统等内容。无论你是初学者还是有经验的用户，都能在这里找到你需要的帮助。𝓳𝓾𝓼𝓽 𝓮𝓷𝓳𝓸𝔂 𝓲𝓽～

!!! info "当前状态 (2026年2月)"
    Zensical 处于 **Alpha**（[PyPI](https://pypi.org/project/zensical/)），核心功能可用，部分能力开发中。详见 [FAQ - 功能状态](faq.md#zensical)。

---

## 导航

<div class="grid cards" markdown>

-   :simple-zenn:{ .lg .middle } __快速开始__

    ---
    
    - [5 分钟快速开始](getting-started/quick-start.md)
    - [命令行接口 (CLI)](getting-started/cli.md)
    - [从 MkDocs 迁移](getting-started/migration.md)
    - [常见问题解答](faq.md)

-   :material-book-open:{ .lg .middle } __核心教程__

    ---
    <!-- - [博客系统完全指南](tutorials/blog-tutorial.md) -->

    - [zensical.toml 配置详解](tutorials/configuration.md)
    - [主题配置指南](tutorials/theme-customization.md)
    - [Markdown 扩展](tutorials/markdown-extensions.md)
    - [Markdown 高效写作](tutorials/zensical-markdown-tip.md)

-   :material-puzzle:{ .lg .middle } __插件系统(暂未开发)__

    ---
    
    - [插件概览](blog/plugins/overview.md)
    - [博客](blog/plugins/blog.md)
    - [搜索](blog/plugins/search.md)
    - [标签](blog/plugins/tags.md)
    - [RSS](blog/plugins/rss.md)

-   :material-rocket:{ .lg .middle } __部署指南__

    ---
    
    - [GitHub Pages（推荐）](blog/deployment/github-pages.md)
    - [Netlify](blog/deployment/netlify.md)
    - [EdgeOne Pages](blog/deployment/edgeone-pages.md)
    - [GitLab Pages](blog/deployment/gitlab-pages.md)
    - [自托管](blog/deployment/self-hosted.md)

</div>


## 推荐学习路径

- **新手**  
  [5 分钟快速开始](getting-started/quick-start.md) → [配置详解](tutorials/configuration.md) → [博客指南](tutorials/blog-tutorial.md) → [主题定制](tutorials/theme-customization.md) → [GitHub Pages 部署](blog/deployment/github-pages.md)
- **从 MkDocs 迁移**  
  [迁移指南](getting-started/migration.md) → [配置差异](tutorials/configuration.md) → 测试后部署
- **进阶**  
  [性能](blog/advanced/performance.md)、[SEO](blog/advanced/seo.md)、[i18n](blog/advanced/i18n.md)、[404/字体/评论](blog/advanced/custom-404.md) 等见「高级主题」

## 快速开始  

![Google Chrome 2026-02-25 18.29.42.png](https://i.imgant.com/v2/7fTK6kG.png)

在项目目录下执行（需 [Python 3.10+](https://pypi.org/project/zensical/)）：

```bash
python3 -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install zensical
zensical new .
zensical serve
```

浏览器打开 [http://localhost:8000](http://localhost:8000) 即可预览。完整步骤见 [5 分钟快速开始](getting-started/quick-start.md)。

常用命令：`zensical serve` 预览，`zensical build --clean` 清理构建。  
更多见 [官方文档](https://zensical.org/docs/)。Zensical 不支持 MkDocs hooks，可用模板覆盖或 JavaScript 替代。

## 案例

- [Wcowin 的博客](https://wcowin.work)
- [Suffine Hub](https://sufine.top/)
- [Beyond欣's Notes](https://notes.beyondxin.top/index.html)
- [更多案例](showcase.md)
- 基于 Mkdocs、Zensical 的主题与站点汇总在：<a href="https://gist.github.com/Wcowin/d36a31b86aec04c203fec1562bb2391b" target="_blank">GitHub Gist</a>(支持评论提交)

![image.png](https://i.imgant.com/v2/OrGeyFz.png)

## 贡献与联系

欢迎 Fork 后提 PR。

- **GitHub**：[Wcowin/Zensical-Chinese-Tutorial](https://github.com/Wcowin/Zensical-Chinese-Tutorial)
- **Email**：[wcowin@qq.com](mailto:wcowin@qq.com)
- 微信与 Telegram 见下方


<center>

<p>微信</p>  
<a href="https://pic3.zhimg.com/80/v2-5ef3dde831c9d0a41fe35fabb0cb8784_1440w.webp" target="_blank">
<img src="https://pic3.zhimg.com/80/v2-5ef3dde831c9d0a41fe35fabb0cb8784_1440w.webp" style="width: 450px; height: auto;">
</a>

<p>Telegram</p>  

<a href="https://t.me/Wcowin" target="_blank">
<img src="https://pica.zhimg.com/80/v2-d5876bc0c8c756ecbba8ff410ed29c14_1440w.webp" style="width: 450px; height: auto;">
</a>

</center>

---

<!--
  将所有页面级脚本和元数据统一放置在这里
-->
<!-- 访问统计区域 -->
<!-- <div style="text-align: center; margin: 2rem 0; font-size: 0.9rem;">
  本站访问量：<script async src="//finicounter.eu.org/finicounter.js"></script><span id="finicount_views" style="font-weight: bold; color: #518FC1;"></span>
</div> -->

<!-- Umami Analytics -->
<script defer src="https://cloud.umami.is/script.js" data-website-id="061b4dea-9b7b-4ffa-9071-74cde70f3dfb"></script>

<style>
/* body::before {
  --size: 35px;
  --line: color-mix(in hsl, canvasText, transparent 80%);
  content: '';
  height: 100vh;
  width: 100%;
  position: absolute;
  background: linear-gradient(
        90deg,
        var(--line) 1px,
        transparent 1px var(--size)
      )
      50% 50% / var(--size) var(--size),
    linear-gradient(var(--line) 1px, transparent 1px var(--size)) 50% 50% /
      var(--size) var(--size);
  -webkit-mask: linear-gradient(-20deg, transparent 50%, white);
          mask: linear-gradient(-20deg, transparent 50%, white);
  top: 80px;
  transform-style: flat;
  pointer-events: none;
  z-index: -1;
} */

@media (max-width: 768px) {
  body::before {
    display: none;
  }
}
</style>

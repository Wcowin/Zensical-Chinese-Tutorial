---
title: 插件概览
date: 2025-02-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 插件系统
---

# 插件概览

> 与官方文档对齐：[Compatibility - Third-party plugins](https://zensical.org/compatibility/plugins/)

Zensical 内置博客、搜索、标签、RSS 等能力，通过配置即可使用，无需像 MkDocs 那样安装第三方插件。后续会通过**模块系统**提供更灵活的扩展方式。

## 本站已文档化的插件

| 插件 | 说明 | 文档 |
|------|------|------|
| 博客 | 文章列表、分类、标签、阅读时间、草稿 | [博客插件详解](blog.md) |
| 搜索 | 站内搜索、建议与高亮 | [搜索插件配置](search.md) |
| 标签 | 标签索引与导航 | [标签插件使用](tags.md) |
| RSS | 订阅源生成 | [RSS 插件配置](rss.md) |

## 与 MkDocs 插件的对应与规划

Zensical 由 Material for MkDocs 原团队开发，对 MkDocs 生态的插件做了定量与定性分析（基于 GitHub 上大量使用 Material 的仓库及 MkDocs 插件目录），并承诺在 Zensical 中**原生提供**相应能力，而不是简单移植插件。

官方在 [Third-party plugins](https://zensical.org/compatibility/plugins/) 中说明了计划覆盖的 MkDocs 插件及思路，例如：

| MkDocs 插件 / 能力 | Zensical 的规划 |
|--------------------|-----------------|
| **mkdocstrings** | 与 mkdocstrings 作者合作，构建专用 API 文档模块 |
| **git-revision-date-localized / git-authors / git-committers** | 原生支持 Git 元数据 |
| **macros** | 通过未来的**组件系统**提供动态内容能力 |
| **minify** | 原生包含压缩、图片优化等构建优化 |
| **mike（多版本文档）** | 提供更灵活的版本管理与工作流 |
| **awesome-nav / literate-nav** | 通过**模块化导航**支持更灵活的信息架构 |
| **static-i18n** | 原生多语言支持 |

!!! info "Zensical Spark"
    新功能会在 [Zensical Spark](https://zensical.org/spark/) 与专业用户一起设计、验证，再集成进 Zensical，而不是简单复刻现有插件。

**完整列表与更新进度**请以官方为准：[Compatibility - Third-party plugins](https://zensical.org/compatibility/plugins/)。未来的**模块系统**将支持第三方扩展，形成可扩展生态。

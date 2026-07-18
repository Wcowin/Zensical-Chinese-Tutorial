---
title: 关于
date: 2025-01-22
---

# 关于 Zensical-Chinese-Tutorial

## 项目简介

Zensical-Chinese-Tutorial 是最详细、最便捷、最前沿的 Zensical 中文教程。

## 与官方文档对齐

本站教程在结构上与 [Zensical 官方](https://zensical.org/) 对齐，便于与官方文档互查。维护者可参考 [与官方文档对齐说明](OFFICIAL_ALIGNMENT.md)（仓库内文档）进行颗粒度同步。

## 路线图与愿景

Zensical 由 Material for MkDocs 原班团队开发，目前处于 **Alpha 阶段**，正在快速迭代。以下是官方路线图要点摘要，完整内容以官方为准。

### 已实现的基础

- **Rust 运行时 (ZRX)**：全新的底层引擎，支持增量构建、任务调度和并发处理
- **Modern / Classic 双主题**：Modern 是全新的现代设计，Classic 完全兼容 Material for MkDocs 外观
- **向后兼容**：原生读取 `mkdocs.yml`，使用 Python Markdown 解析器保证方言一致，内置 MiniJinja 模板引擎实现并行渲染
- **Studio 编辑器**：专属写作环境，支持实时链接检测和智能提示
- **即时导航**：无刷新页面切换，开箱即用

### 即将到来的能力

- **模块化架构**：将构建管线拆分为可组合、可扩展的模块，支持显式依赖和智能缓存，提供 Python 连接器
- **Disco 搜索引擎**：全新搜索内核，支持倒排索引、向量查询和联邦搜索，未来将作为独立开源项目发布
- **UI 组件框架**：用独立组件替代传统模板，每个组件自包含数据获取、渲染、样式和交互逻辑
- **配置管理革新**：支持零配置默认值、代码化配置、Monorepo 支持和可复用预设
- **灵活导航系统**：从单体导航转向内容驱动的可扩展导航，配合智能缓存
- **嵌套项目**：支持多层级目录结构、跨项目链接、统一搜索和灵活部署
- **全球化本地化**：灵活的内容组织方式、机器学习辅助翻译草稿、完整的界面和代码片段翻译
- **发布追踪**：支持基于 Git 或文件夹的版本管理，增量重建只处理变更内容
- **主题导向写作**：支持内容复用、DITA 兼容、多变体发布，以及为 LLM/AI 助手优化的上下文生成

### 官方链接

- **[Roadmap](https://zensical.org/about/roadmap/)**：完整路线图与进展追踪
- **[Vision](https://zensical.org/about/vision/)**：产品愿景与社区协作方式
- **[Newsletter](https://zensical.org/about/newsletter/)**：月度进展与动态
- **[Zensical Spark](https://zensical.org/about/)**：高级支持与早期功能访问

## 共同作者

**Wcowin**

- GitHub: [@Wcowin](https://github.com/Wcowin)
- Email: [wcowin@qq.com](mailto:wcowin@qq.com)
- Telegram: [@Wcowin](https://t.me/Wcowin)

**jaywhj**

- GitHub: [@jaywhj](https://github.com/jaywhj)
- Email: [junewhj@qq.com](mailto:junewhj@qq.com)

**Luwei**

- GitHub: [@Luwei](https://github.com/weigo6)
- Email: [yang92636@qq.com](mailto:yang92636@qq.com)


## 贡献

欢迎参与项目完善！

<a href="https://github.com/Wcowin/Zensical-Chinese-Tutorial/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Wcowin/Zensical-Chinese-Tutorial" />
</a>

## License

Copyright (c) 2025-2026 Wcowin

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

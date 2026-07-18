---
title: Zensical Studio 使用指南
date: 2026-06-25
---

# Zensical Studio 使用指南

> 像重构代码一样重构文档

[Zensical Studio](https://zensical.org/studio/) 是 Zensical 官方提供的 **VS Code 扩展**，目前处于公开测试阶段，免费使用。它直接集成在编辑器中，帮助你实时检测文档问题、安全重构文档结构，让写文档的体验接近写代码。

## 为什么需要 Studio？

用 Markdown 写文档时，你可能遇到过这些痛点：

- 移动或重命名了一个文件，结果一堆链接断了
- 修改了某个标题，但引用它的地方没有同步更新
- 文档越写越多，不知道哪些链接已经失效

Studio 就是为了解决这些问题而生的。它能**即时发现断链**，在你重构文件时**自动更新所有引用**，让你放心大胆地调整文档结构。

## 核心功能

### 断链即时检测

Studio 会实时扫描你的文档项目，一旦发现断裂的超链接或无效引用，立刻标记出来。不用等到构建时才发现错误。

### 安全重构

当你移动、重命名或重组文件时，Studio 会自动同步更新所有相关的：

- 内部链接
- 标题引用
- 导航结构

这就像 IDE 里的"重命名符号"功能，只不过是针对 Markdown 文档的。

### Python Markdown 语法高亮

Studio 提供了针对 Python Markdown 方言的精准语法高亮，包括 Zensical/Material for MkDocs 特有的扩展语法（如 admonition、content tabs、code annotations 等），比普通 Markdown 高亮更准确。

### 文档导航

在编辑器内提供文档结构导航，快速跳转到任意标题或文件，在大型文档项目中尤其有用。

### 兼容性

Studio 同时支持 **Zensical 项目**和 **MkDocs 项目**，如果你还在用 MkDocs，也可以直接装上试试。

## 安装

### 前置要求

- **VS Code** 版本 1.100.0 或更新
- 支持平台：Windows (x64/ARM)、macOS (Intel/Apple Silicon)、Linux (x64/ARM64)

### 安装步骤

1. 打开 VS Code
2. 按 `Ctrl+Shift+X`（macOS: `Cmd+Shift+X`）打开扩展面板
3. 搜索 **Zensical Studio**
4. 点击 **Install**

或者直接访问 [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=zensical.zensical-studio) 安装。

## 基本使用

安装完成后，用 VS Code 打开你的 Zensical 或 MkDocs 项目即可。Studio 会自动识别项目结构并开始工作：

- 编辑 Markdown 文件时，断链会被实时标记
- 在 VS Code 文件管理器中移动或重命名 `.md` 文件时，Studio 会自动提示更新引用
- 语法高亮会自动适配 Python Markdown 方言

### 启用 Python Markdown 语言模式

为了获得最佳的语法高亮效果，建议在项目根目录创建或编辑 `.vscode/settings.json`，添加以下配置：

```json
{
  "files.associations": {
    "*.md": "python-markdown"
  }
}
```

这会让 VS Code 将 `.md` 文件识别为 Python Markdown 格式，Studio 的语法高亮就能覆盖所有 Zensical 特有的扩展语法。

## 实用建议

- **写文档前先开着 Studio**：实时检测比事后修复省事得多
- **大胆重构**：有了自动引用更新，你可以放心调整目录结构和文件名
- **团队协作**：建议把 `.vscode/settings.json` 提交到仓库，让团队成员都能获得一致的体验

## 了解更多

- **官方页面**：[Zensical Studio](https://zensical.org/studio/)
- **扩展市场**：[VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=zensical.zensical-studio)
- **反馈问题**：通过 [GitHub Issues](https://github.com/Wcowin/Zensical-Chinese-Tutorial/issues) 或官方渠道反馈

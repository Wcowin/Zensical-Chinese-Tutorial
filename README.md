# Zensical 中文教程

> 🚀 最详细、最便捷、最前沿的 Zensical 中文教程

[![Built with Zensical](https://img.shields.io/badge/Built_with-Zensical-4051B5?style=flat-square)](https://zensical.org/)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](LICENSE)

**在线阅读**：[https://wcowin.work/Zensical-Chinese-Tutorial/](https://wcowin.work/Zensical-Chinese-Tutorial/)

## 为什么选择 Zensical？

- ✅ MkDocs 已停止更新，Zensical 是官方推荐的新一代
- ✅ 即时导航，无需刷新页面
- ✅ 博客系统，开箱即用
- ✅ Rust 运行时，性能优异
- ✅ Modern/Classic 双主题

## 快速开始

```bash
# 克隆项目
git clone https://github.com/Wcowin/Zensical-Chinese-Tutorial.git
cd Zensical-Chinese-Tutorial

# 创建虚拟环境
python3 -m venv .venv
source .venv/bin/activate  # macOS/Linux
# .venv\Scripts\activate   # Windows

# 安装依赖
pip install -r requirements.txt

# 启动预览
zensical serve
```

打开浏览器访问 `http://127.0.0.1:8000`

## 教程内容

| 分类 | 内容 |
|------|------|
| **快速开始** | 5分钟快速开始、从 MkDocs 迁移 |
| **核心教程** | 配置详解、主题定制、Markdown 扩展、博客系统 |
| **插件系统** | 博客、搜索、标签、RSS |
| **部署指南** | GitHub Pages、Netlify、GitLab Pages、自托管 |
| **高级主题** | 性能优化、SEO、多语言、评论系统 |

## 项目结构

```
├── docs/                  # 文档源文件
│   ├── index.md          # 首页
│   ├── getting-started/  # 快速开始
│   ├── tutorials/        # 核心教程
│   └── blog/             # 博客相关
├── zensical.toml         # 配置文件
└── requirements.txt      # 依赖
```

## 部署

```bash
# 构建
zensical build --clean

# 部署到 GitHub Pages（推荐）
# 详见：docs/blog/deployment/github-pages.md
```

## 联系方式

- **GitHub**: [@Wcowin](https://github.com/Wcowin)
- **Email**: wcowin@qq.com
- **Telegram**: [@Wcowin](https://t.me/Wcowin)

## 贡献

欢迎提交 Issue 和 Pull Request！

## License

Copyright (c) 2025-2026 Wcowin

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

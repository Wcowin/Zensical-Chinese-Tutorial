---
title: 命令行接口 (CLI)
date: 2025-02-22
authors:
  - name: Wcowin
    email: wcowin@qq.com
categories:
  - 快速开始
---

# 命令行接口 (CLI)

> 与官方文档对齐：[Usage - CLI](https://zensical.org/docs/usage/cli/) | [Compatibility - Command line interface](https://zensical.org/compatibility/cli/)

Zensical 在命令行中使用 `zensical` 替代 `mkdocs`，语法形式为：

```bash
zensical COMMAND [OPTIONS] [ARGS]...
```

## 常用命令

| 命令 | 说明 | 官方文档 |
|------|------|----------|
| `zensical serve` | 启动本地预览服务器 | [preview](https://zensical.org/docs/usage/preview/) |
| `zensical build` | 构建静态站点 | [build](https://zensical.org/docs/usage/build/) |
| `zensical new` | 创建新项目 | [new](https://zensical.org/docs/usage/new/) |

查看帮助：`zensical --help` 或针对某命令 `zensical build --help`。

## 与 MkDocs 的差异

若你从 MkDocs / Material for MkDocs 迁移，需注意以下命令行差异，并相应调整构建或 CI 脚本：

| 项目 | MkDocs | Zensical |
|------|--------|----------|
| 命令名 | `mkdocs` | `zensical` |
| `--theme` / `-t` | 支持 | **不支持**（当前仅提供单一主题，未来模块系统会扩展） |
| `--use-directory-urls` / `--no-directory-urls` | 支持 | **不支持**，请在配置文件中设置 `use_directory_urls` |
| `--site-dir` | 支持 | **不支持**，请在配置文件中设置 `site_dir` |
| `--strict` | 支持 | 当前**被忽略**，后续会加入配置与链接校验 |
| `serve --dirty` | 支持 | **不需要**，Zensical 默认使用缓存以加速 |
| `gh-deploy` | 支持 | **不提供**，请使用 [GitHub Actions 等部署方式](https://zensical.org/docs/publish-your-site/) |
| `get-deps` | 支持 | **不支持**，建议在 `pyproject.toml` 中声明依赖 |

## 配置优先

以下行为均由 **配置文件** 控制，不要依赖命令行参数：

- **主题**：在 `zensical.toml` 的 `[project.theme]` 中设置（如 `variant = "modern"`）。
- **目录 URL**：在 `[project]` 中设置 `use_directory_urls = true/false`。
- **输出目录**：在 `[project]` 中设置 `site_dir = "site"`（或如 GitLab Pages 所需的 `public`）。

## 延伸阅读

- 官方 [Usage - CLI](https://zensical.org/docs/usage/cli/)
- 官方 [Compatibility - Command line interface](https://zensical.org/compatibility/cli/)
- 本站 [5 分钟快速开始](quick-start.md)、[从 MkDocs 迁移](migration.md)

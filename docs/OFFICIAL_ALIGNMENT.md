# Zensical 中文教程与官方文档对齐说明

> 本文档对比 [Zensical 官方](https://zensical.org/) 与本站教程的颗粒度，便于维护时与官方保持一致。  
> 官方入口：[https://zensical.org/](https://zensical.org/) | 官方文档：[https://zensical.org/docs/](https://zensical.org/docs/) | 兼容性：[https://zensical.org/compatibility/](https://zensical.org/compatibility/)

---

## 一、官方站点结构概览

根据 [zensical.org](https://zensical.org/) 当前结构，大致分为：

| 官方板块 | 路径 | 主要内容 |
|----------|------|----------|
| **Documentation** | `/docs/` | 使用与配置文档 |
| **Get started** | `/docs/get-started/` | 安装（pip / uv / Docker）、前置条件 |
| **Setup** | `/docs/setup/` | 项目配置基础 |
| **Usage** | `/docs/usage/` | 命令行使用 |
| **Authoring** | `/docs/authoring/` | 写作与 Markdown |
| **Publish** | `/docs/publish-your-site/` | 发布与部署 |
| **Compatibility** | `/compatibility/` | 与 MkDocs 的兼容说明 |
| **About** | `/about/` | 产品介绍、路线图、团队等 |

---

## 二、官方 vs 中文教程 颗粒度对照

### 2.1 入门与安装（Get started）

| 官方 | 中文教程 | 对齐情况 |
|------|----------|----------|
| [Get started](https://zensical.org/docs/get-started/)：安装（pip / uv / Docker）、前置条件、Python 虚拟环境 | [5 分钟快速开始](getting-started/quick-start.md) | ✅ 已覆盖 pip 安装与基本步骤；建议在「安装」小节显式区分 **pip / uv / Docker** 三种方式，并与官方子节对应；可增加「使用 Docker」简短说明 + 链接 [Docker Hub](https://hub.docker.com/r/zensical/zensical) |

### 2.2 配置基础（Setup / Configuration）

| 官方 | 中文教程 | 对齐情况 |
|------|----------|----------|
| [Setup > Basics](https://zensical.org/docs/setup/basics/)：`zensical.toml`、项目作用域、主题变体、各 settings（site_name, site_url, site_description, site_author, copyright, docs_dir, site_dir, extra, use_directory_urls, dev_addr）、不支持的设置 | [zensical.toml 配置详解](tutorials/configuration.md) | ✅ 内容已很全；建议在目录或文内小节上与官方 Basics 的「主题变体」「Settings」「Unsupported settings」等子节对应，便于读者与官方互查 |
| [Compatibility > Configuration](https://zensical.org/compatibility/configuration/)：Zensical 如何理解 `mkdocs.yml`、模块与兼容层 | [从 MkDocs 迁移](getting-started/migration.md) | ⚠️ 建议在迁移篇中增加一小节「兼容：继续使用 mkdocs.yml」，并链接到官方 Configuration 页 |

### 2.3 命令行（CLI / Usage）

| 官方 | 中文教程 | 对齐情况 |
|------|----------|----------|
| [Compatibility > Command line interface](https://zensical.org/compatibility/cli/)：`zensical` 与 `mkdocs` 的差异（如 `--theme`、`--site-dir`、`gh-deploy`、`get-deps` 等） | 分散在快速开始、各教程中 | ❌ **缺失**：建议新增 **「命令行接口」** 独立页，包含：与 mkdocs 的差异、`serve` / `build` / `new` 的简要说明、链接到 [docs/usage/cli](https://zensical.org/docs/usage/cli/) 与 [compatibility/cli](https://zensical.org/compatibility/cli/) |
| [Usage](https://zensical.org/docs/usage/cli/)：`serve`、[build](https://zensical.org/docs/usage/build/)、[new](https://zensical.org/docs/usage/new/) | [使用 Markdown 高效写作](tutorials/zensical-markdown-tip.md) 等有零散命令引用 | ✅ 可保留现状；新建的「命令行接口」页统一收口并链到官方 Usage |

### 2.4 写作与 Markdown（Authoring）

| 官方 | 中文教程 | 对齐情况 |
|------|----------|----------|
| [Authoring](https://zensical.org/docs/authoring/markdown/)：admonitions、code-blocks、content-tabs、diagrams、footnotes、formatting、icons-emojis、math、lists/task lists、tooltips、frontmatter 等 | [Markdown 扩展使用](tutorials/markdown-extensions.md)、[使用 Markdown 高效写作](tutorials/zensical-markdown-tip.md) | ✅ 颗粒度基本对齐；建议在每类语法旁注明「对应官方：authoring/xxx」，便于中英对照 |

### 2.5 主题与定制（Theme / Customization）

| 官方 | 中文教程 | 对齐情况 |
|------|----------|----------|
| [Customization](https://zensical.org/docs/customization/)（若存在）、Setup 中的 theme variant | [主题定制指南](tutorials/theme-customization.md) | ✅ 已有；保持与官方「modern / classic」及配置项一致即可 |

### 2.6 发布与部署（Publish）

| 官方 | 中文教程 | 对齐情况 |
|------|----------|----------|
| [Publish your site](https://zensical.org/docs/publish-your-site/)：GitHub Pages（Actions）、GitLab Pages | [GitHub Pages 部署](blog/deployment/github-pages.md)、[GitLab Pages 部署](blog/deployment/gitlab-pages.md) 等 | ✅ 中文更细（含 Netlify、EdgeOne、自托管等）；建议在首页或部署章节总览中注明「对应官方：Publish your site」 |

### 2.7 兼容性与功能（Compatibility）

| 官方 | 中文教程 | 对齐情况 |
|------|----------|----------|
| [Compatibility 总览](https://zensical.org/compatibility/)：何谓兼容、分阶段策略 | 迁移、配置中有提及 | ⚠️ 建议在「关于」或「常见问题」中增加「与 MkDocs 的兼容策略」摘要 + 链接 |
| [Feature parity](https://zensical.org/compatibility/features/)：功能对照表（Core、Site structure、Appearance、Markdown extensions、Content、Navigation、Optimization、Extensions） | [FAQ](faq.md) 等有零散说明 | ❌ **缺失**：建议新增 **「功能对照表」** 页或 FAQ 子节：简要列出与 Material for MkDocs 的对应关系，并链到官方 feature parity 表 |
| [Third-party plugins](https://zensical.org/compatibility/plugins/)：mkdocstrings、git 相关、macros、minify、mike、awesome-nav、static-i18n 等计划 | [插件系统](blog/plugins/)：博客、搜索、标签、RSS | ⚠️ 建议在插件总览中增加「与 MkDocs 插件的对应与规划」小节，链到官方 plugins 页 |

### 2.8 关于与路线图（About）

| 官方 | 中文教程 | 对齐情况 |
|------|----------|----------|
| [About](https://zensical.org/about/)、[Roadmap](https://zensical.org/about/roadmap/)、Vision、Team、Newsletter | [关于](about.md) | ⚠️ 建议在关于页中增加「路线图 / 愿景」摘要 + 官方 Roadmap/Vision 链接，保持与官方表述同步 |

---

## 三、建议新增/调整的颗粒度

1. **新增「命令行接口」页**（如 `docs/getting-started/cli.md`）  
   - 说明 `zensical` 与 `mkdocs` 的差异（参考 [compatibility/cli](https://zensical.org/compatibility/cli/)）。  
   - 简要列出 `serve`、`build`、`new` 及常用选项，并链到 [docs/usage/cli](https://zensical.org/docs/usage/cli/)。

2. **新增「功能对照表」页或 FAQ 子节**  
   - 对应 [Feature parity](https://zensical.org/compatibility/features/)：用表格或列表概括 Core / Site / Appearance / Markdown / Content / Navigation / Optimization，并注明「详见官方」。

3. **快速开始**  
   - ✅ 已按「pip / uv / Docker」拆分子节并补充 Docker 说明与 Docker Hub 链接。

4. **迁移篇**  
   - 增加「兼容：继续使用 mkdocs.yml」小节，链到 [Compatibility > Configuration](https://zensical.org/compatibility/configuration/)。

5. **关于页**  
   - 增加「路线图与愿景」摘要，链到 [Roadmap](https://zensical.org/about/roadmap/)、[Vision](https://zensical.org/about/vision/)。

6. **插件总览**  
   - ✅ 已新增 [插件概览](blog/plugins/overview.md)，含「与 MkDocs 插件的对应与规划」及官方 Third-party plugins 链接。

---

## 四、官方链接速查

| 用途 | 链接 |
|------|------|
| 文档首页 | https://zensical.org/docs/ |
| 入门安装 | https://zensical.org/docs/get-started/ |
| 配置基础 | https://zensical.org/docs/setup/basics/ |
| 命令行用法 | https://zensical.org/docs/usage/cli/ |
| CLI 兼容差异 | https://zensical.org/compatibility/cli/ |
| 配置兼容 | https://zensical.org/compatibility/configuration/ |
| 功能对照 | https://zensical.org/compatibility/features/ |
| 第三方插件 | https://zensical.org/compatibility/plugins/ |
| 发布站点 | https://zensical.org/docs/publish-your-site/ |
| 关于 / 路线图 | https://zensical.org/about/ ， https://zensical.org/about/roadmap/ |

---

*文档最后更新与官方结构核对：2025-02。若官方结构调整，请以 zensical.org 为准并同步更新本对齐说明。*

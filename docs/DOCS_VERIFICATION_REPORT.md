# 文档校验报告

> 基于联网与官方文档核对后的结论，供维护参考。最后校验：2026-02-22。

## 已修正的问题

### 1. Python 版本要求（已修正）

- **问题**：多处写「Python 3.8 或更高」「推荐 3.9+」，与 [PyPI](https://pypi.org/project/zensical/) 当前要求不符。
- **官方**：PyPI 标明 **Python: >=3.10**。
- **已修改**：
  - `docs/getting-started/quick-start.md`：改为「Python 3.10 或更高」「推荐 3.11+」，并链到 PyPI。
  - `docs/faq.md`：改为「Python 3.10 或更高」「推荐 3.11+」，并链到 PyPI。
  - `docs/blog/deployment/netlify.md`：说明 Zensical 需 3.10+，建议 `runtime.txt` 写 3.10 或 3.11。
  - `docs/blog/deployment/github-pages.md`：在 workflow 注释中注明「Zensical 需 Python 3.10+」。

### 2. Zensical 阶段表述（已修正）

- **问题**：首页曾写「Beta 阶段」。
- **官方**：PyPI 标明 **Status: 3 - Alpha**。
- **已修改**：`docs/index.md` 改为「Alpha 阶段」，并链到 PyPI 状态页。

### 3. Netlify 默认 Python（已修正）

- **问题**：写「Netlify 默认使用 Python 3.8」且仅示例 3.11。
- **已修改**：说明 Zensical 需 3.10+，建议用 `runtime.txt` 指定 3.10 或 3.11，并链到 PyPI。

---

## 已核对为正确的项

| 项目 | 核对结果 |
|------|----------|
| 官方文档链接（zensical.org/docs、get-started、compatibility、roadmap 等） | 可访问，内容一致 |
| uv 文档链接（docs.astral.sh/uv） | 可访问 |
| Docker 镜像（hub.docker.com/r/zensical/zensical） | 存在 |
| GitHub Actions 工作流（configure-pages@v5、checkout@v5、setup-python@v5、upload-pages-artifact@v4、deploy-pages@v4） | 与 [官方 Publish your site](https://zensical.org/docs/publish-your-site/) 一致 |
| `zensical build --clean` | 与官方推荐一致 |
| 配置项（site_name、site_url、[project] 作用域、TOML 顺序等） | 与 [Setup > Basics](https://zensical.org/docs/setup/basics/) 一致 |
| Admonitions 等 Authoring 链接 | 可访问 |
| FAQ / 关于中的 Alpha 表述 | 与 PyPI 一致 |

---

## 建议后续定期核对

1. **Python 版本**：在 [PyPI - zensical](https://pypi.org/project/zensical/) 查看「Python」要求，若变更需同步更新快速开始、FAQ、Netlify、GitHub Pages 等。
2. **阶段（Alpha/Beta/Stable）**：以 PyPI 的「Status」或官方公告为准，同步首页与 FAQ。
3. **GitHub Actions 版本**：官方若更新 `actions/configure-pages@v5`、`actions/setup-python@v5` 等，同步更新部署文档与 `.github/workflows/docs.yml`。
4. **官方文档 URL**：若 zensical.org 改版或路径变更，需更新本站链接与 [OFFICIAL_ALIGNMENT.md](OFFICIAL_ALIGNMENT.md)。

---

*本报告由人工+联网核对生成，如有遗漏以官方为准。*

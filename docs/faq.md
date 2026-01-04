# 常见问题解答 (FAQ)

> 解决 Zensical 使用中的常见问题

## Zensical 功能状态

!!! info "当前版本状态"
    Zensical 目前处于 **Alpha 阶段**，正在快速迭代中。以下是功能状态概览：
    
    | 功能 | 状态 | 说明 |
    |------|------|------|
    | 核心构建 | ✅ 可用 | Rust 运行时，高性能构建 |
    | 主题系统 | ✅ 可用 | Modern/Classic 双主题 |
    | Markdown 扩展 | ✅ 可用 | 完整的 Python Markdown 支持 |
    | 即时导航 | ✅ 可用 | 无刷新页面切换 |
    | 搜索功能 | ✅ 可用 | 内置搜索（Disco 引擎开发中） |
    | 博客系统 | ⚠️ 开发中 | Feature Parity 阶段 |
    | 标签系统 | ⚠️ 开发中 | Feature Parity 阶段 |
    | RSS 订阅 | ⚠️ 开发中 | Feature Parity 阶段 |
    | 多语言 (i18n) | 🔜 规划中 | Roadmap 功能 |
    | 版本管理 | 🔜 规划中 | Roadmap 功能 |
    | 模块系统 | 🔜 规划中 | 替代传统插件 |
    | 组件系统 | 🔜 规划中 | 替代模板系统 |
    
    详细信息请查看 [Zensical Roadmap](https://zensical.org/about/roadmap/)。

## 安装相关

### 如何安装 Zensical？

推荐使用虚拟环境安装：

```bash
# 创建虚拟环境
python3 -m venv .venv

# 激活虚拟环境
source .venv/bin/activate  # macOS/Linux
# 或 .venv\Scripts\activate  # Windows

# 安装 Zensical
pip install zensical
```

详细步骤请参考 [5 分钟快速开始](getting-started/quick-start.md)。

### 安装后提示 `command not found: zensical` 怎么办？

这通常是因为虚拟环境未激活。请确保：

1. 已创建虚拟环境
2. 已激活虚拟环境
3. 在激活的虚拟环境中安装了 Zensical

### Zensical 需要什么 Python 版本？

Zensical 需要 Python 3.8 或更高版本。推荐使用 Python 3.9+。

## 配置相关

### `site_name` 是必需的吗？

是的，`site_name` 目前是必需的配置项。这是因为 Zensical 替换的 MkDocs 需要它。未来版本可能会使其可选。

### 如何设置中文界面？

在 `zensical.toml` 中设置：

```toml
[project.theme]
language = "zh"
```

### 可以使用 mkdocs.yml 配置文件吗？

可以！Zensical 原生支持读取 `mkdocs.yml` 文件，方便从 MkDocs 迁移。但建议新项目使用 `zensical.toml`。

## 主题相关

### modern 和 classic 主题有什么区别？

- **modern**：全新的现代设计，Zensical 的默认主题
- **classic**：完全匹配 Material for MkDocs 的外观和感觉

切换主题：

```toml
[project.theme]
variant = "modern"  # 或 "classic"
```

### 如何自定义主题？

1. 创建 `docs/overrides` 目录
2. 在 `zensical.toml` 中启用：

```toml
[project.theme]
custom_dir = "docs/overrides"
```

3. 在 `overrides` 目录中覆盖模板文件

## 功能相关

### 如何启用即时导航？

即时导航默认启用。如需配置：

```toml
[project.theme]
features = [
    "navigation.instant",           # 即时导航
    "navigation.instant.prefetch",  # 预加载
]
```

!!! warning "重要"
    即时导航需要设置 `site_url`：
    
    ```toml
    [project]
    site_url = "https://example.com"
    ```

### 如何添加博客功能？

!!! warning "功能状态"
    博客功能目前在 Feature Parity 阶段开发中，配置方式可能会有变化。

Zensical 内置博客插件，只需配置即可：

```toml
[project.plugins.blog]
post_date_format = "full"
draft = true
post_readtime = true
post_readtime_words_per_minute = 265  # 中文适配
```

详细教程请参考 [博客系统完全指南](tutorials/blog-tutorial.md)。

### 支持数学公式吗？

支持！启用 MathJax：

```toml
[project.markdown_extensions."pymdownx.arithmatex"]
generic = true
```

然后在 `extra_javascript` 中添加 MathJax：

```toml
extra_javascript = [
    "javascripts/mathjax.js",
    "https://unpkg.com/mathjax@3/es5/tex-mml-chtml.js"
]
```

## 部署相关

### 如何部署到 GitHub Pages？

1. 构建网站：`zensical build`
2. 将 `site/` 目录内容推送到 GitHub
3. 在仓库设置中启用 GitHub Pages

详细步骤请参考 [GitHub Pages 部署](blog/deployment/github-pages.md)。

### 推荐的部署方式是什么？

推荐使用 **GitHub Pages**，因为：

- ✅ **完全免费** - 无需任何费用
- ✅ **自动 HTTPS** - 免费 SSL 证书
- ✅ **GitHub 集成** - 与仓库无缝集成
- ✅ **简单易用** - 推送即部署
- ✅ **自定义域名** - 支持绑定域名

详细步骤请参考 [GitHub Pages 部署](blog/deployment/github-pages.md)。

## 迁移相关

### 从 MkDocs 迁移难吗？

非常简单！Zensical 设计时就考虑了兼容性：

1. 可以直接使用现有的 `mkdocs.yml`
2. HTML 结构与 Material for MkDocs 匹配
3. 大部分插件都有对应实现

详细指南请参考 [从 MkDocs 迁移到 Zensical](getting-started/migration.md)。

### MkDocs hooks 不支持怎么办？

Zensical 不支持 MkDocs hooks。替代方案：

- **模板覆盖** - 用于修改 HTML 结构
- **自定义 JavaScript** - 用于动态行为
- **构建脚本** - 用于预处理

Zensical 正在开发模块系统来替代 hooks。

## 错误处理

### 提示 "No such file or directory" 错误

检查以下几点：

1. `docs_dir` 配置是否正确（默认为 `docs`）
2. 导航配置中的文件路径是否存在
3. `custom_dir` 目录是否存在（如果配置了）

### 构建失败怎么办？

1. 检查配置文件语法是否正确
2. 确保所有引用的文件都存在
3. 查看错误信息中的具体提示
4. 使用 `zensical build --verbose` 获取详细日志

### 样式显示不正常

1. 清理构建缓存：`zensical build --clean`
2. 检查 `extra_css` 文件路径是否正确
3. 确保 CSS 文件语法正确

## 性能相关

### 如何提升网站性能？

1. **启用即时导航**：减少页面加载时间
2. **使用 CDN**：加速静态资源加载
3. **优化图片**：压缩图片大小
4. **启用缓存**：配置适当的缓存策略

详细指南请参考 [性能优化](blog/advanced/performance.md)。

## 其他问题

### 在哪里可以获取帮助？

- **官方文档**：[https://zensical.org/docs/](https://zensical.org/docs/)
- **本教程**：[Zensical 中文教程](https://wcowin.work/Zensical-Chinese-Tutorial/)
- **社区支持**：[Zensical-Chinese-Tutorial 社区](https://support.qq.com/products/646913/)
- **GitHub Issues**：[提交问题](https://github.com/Wcowin/Zensical-Chinese-Tutorial/issues)

### 如何贡献到本教程？

欢迎贡献！

1. Fork 本仓库
2. 创建你的特性分支
3. 提交你的修改
4. 推送到分支
5. 创建 Pull Request

---

**还有其他问题？** 请访问 [Zensical 官方文档](https://zensical.org/docs/) 或在 [社区](https://support.qq.com/products/646913/) 提问。

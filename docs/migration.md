# 从 MkDocs 迁移到 Zensical

> 平滑过渡到下一代文档工具

## 为什么迁移到 Zensical？

Zensical 是由 [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/) 的创建者开发的新一代静态网站生成器。它继承了 Material for MkDocs 的所有优点，并提供了更多现代化功能：

- ✅ **积极维护** - MkDocs 已停止更新，Zensical 是官方推荐的替代方案
- ✅ **即时导航** - 原生支持，无需额外插件
- ✅ **现代主题** - 全新的 modern 主题变体
- ✅ **更好的性能** - 使用 Rust 和 Python 构建，速度更快
- ✅ **TOML 配置** - 比 YAML 更清晰、更不易出错
- ✅ **向后兼容** - 支持读取 `mkdocs.yml` 配置文件

## 迁移概览

迁移过程非常简单，因为 Zensical 设计时就考虑了与 Material for MkDocs 的兼容性：

1. **安装 Zensical**
2. **配置文件迁移**（可选）
3. **测试和调整**
4. **重新部署**

## 第一步：安装 Zensical

在你的项目目录中，安装 Zensical：

=== "使用现有虚拟环境"

    ```bash
    # 激活现有虚拟环境
    source venv/bin/activate  # macOS/Linux
    # 或
    venv\Scripts\activate  # Windows
    
    # 安装 Zensical
    pip install zensical
    ```

=== "创建新虚拟环境"

    ```bash
    # 创建虚拟环境
    python3 -m venv .venv
    
    # 激活虚拟环境
    source .venv/bin/activate  # macOS/Linux
    # 或
    .venv\Scripts\activate  # Windows
    
    # 安装 Zensical
    pip install zensical
    ```

## 第二步：配置文件迁移

Zensical 可以直接读取 `mkdocs.yml` 文件，所以你可以：

### 选项 A：继续使用 mkdocs.yml（推荐用于快速迁移）

无需任何更改，Zensical 会自动读取你的 `mkdocs.yml` 文件：

```bash
# 直接使用现有配置
zensical serve
```

!!! success "即时迁移"
    这是最快的迁移方式。你的网站应该能立即工作，无需任何配置更改。

### 选项 B：转换为 zensical.toml（推荐用于新项目）

虽然 Zensical 支持 `mkdocs.yml`，但我们建议新项目使用 `zensical.toml`。

#### YAML 到 TOML 转换示例

**原 mkdocs.yml：**

```yaml
site_name: 我的文档
site_url: https://example.com
site_author: 张三
site_description: 我的文档网站

theme:
  name: material
  language: zh
  features:
    - navigation.instant
    - navigation.tracking
    - search.suggest
  palette:
    - scheme: default
      primary: indigo
      accent: indigo

plugins:
  - search:
      lang:
        - zh
        - en
  - blog:
      blog_dir: blog

markdown_extensions:
  - admonition
  - pymdownx.highlight:
      anchor_linenums: true
  - pymdownx.superfences

nav:
  - Home: index.md
  - 快速开始: quick-start.md
  - 配置: configuration.md
```

**转换后的 zensical.toml：**

```toml
[project]
site_name = "我的文档"
site_url = "https://example.com"
site_author = "张三"
site_description = "我的文档网站"

[project.theme]
language = "zh"
features = [
    "navigation.instant",
    "navigation.tracking",
    "search.suggest",
]

[[project.theme.palette]]
scheme = "default"
primary = "indigo"
accent = "indigo"

[project.plugins.search]
lang = ["zh", "en"]

[project.plugins.blog]
blog_dir = "blog"

[project.markdown_extensions]
admonition = {}
pymdownx.highlight = { anchor_linenums = true }
pymdownx.superfences = {}

[[project.nav]]
Home = "index.md"

[[project.nav]]
"快速开始" = "quick-start.md"

[[project.nav]]
"配置" = "configuration.md"
```

## 第三步：主题变体选择

Zensical 提供两种主题变体：

### Classic 变体（推荐用于迁移）

如果你想保持与 Material for MkDocs 完全相同的外观：

=== "zensical.toml"

    ```toml
    [project.theme]
    variant = "classic"
    ```

=== "mkdocs.yml"

    ```yaml
    theme:
      variant: classic
    ```

### Modern 变体（推荐用于新项目）

如果你想尝试全新的现代设计：

=== "zensical.toml"

    ```toml
    [project.theme]
    variant = "modern"  # 默认值
    ```

=== "mkdocs.yml"

    ```yaml
    theme:
      variant: modern
    ```

## 第四步：测试网站

启动开发服务器测试你的网站：

```bash
zensical serve
```

在浏览器中打开 [http://localhost:8000](http://localhost:8000) 检查：

- ✅ 所有页面正常显示
- ✅ 导航结构正确
- ✅ 搜索功能工作
- ✅ 博客文章显示正常
- ✅ 自定义 CSS/JS 生效

## 第五步：构建和部署

构建静态网站：

```bash
zensical build
```

生成的文件位于 `site/` 目录，可以部署到任何静态网站托管服务。

## 常见问题和解决方案

### 1. 插件兼容性

大多数 Material for MkDocs 插件在 Zensical 中都有对应的实现：

| MkDocs 插件 | Zensical 支持 | 说明 |
|------------|--------------|------|
| search | ✅ 内置 | 原生支持 |
| blog | ✅ 内置 | 原生支持 |
| tags | ✅ 内置 | 原生支持 |
| social | ✅ 内置 | 原生支持 |
| rss | ✅ 内置 | 原生支持 |

### 2. Hooks 不支持

!!! warning "重要变化"
    Zensical 不支持 MkDocs hooks。如果你的项目使用了 hooks，需要使用以下替代方案：
    
    - **模板覆盖** - 用于修改 HTML 结构
    - **自定义 JavaScript** - 用于动态行为
    - **构建脚本** - 用于预处理

### 3. 自定义 CSS 和 JavaScript

自定义样式和脚本的方式保持不变：

=== "zensical.toml"

    ```toml
    [project]
    extra_css = ["stylesheets/extra.css"]
    extra_javascript = ["javascripts/extra.js"]
    ```

=== "mkdocs.yml"

    ```yaml
    extra_css:
      - stylesheets/extra.css
    extra_javascript:
      - javascripts/extra.js
    ```

### 4. 目录结构

Zensical 使用与 MkDocs 相同的目录结构：

```
.
├── docs/
│   ├── index.md
│   ├── blog/
│   ├── assets/
│   ├── stylesheets/
│   └── javascripts/
├── zensical.toml  # 或 mkdocs.yml
└── site/  # 构建输出
```

### 5. GitHub Actions 更新

如果你使用 GitHub Actions 部署，需要更新工作流：

**原 MkDocs 工作流：**

```yaml
- name: Install dependencies
  run: pip install mkdocs-material
- name: Build site
  run: mkdocs build
```

**更新为 Zensical：**

```yaml
- name: Install dependencies
  run: pip install zensical
- name: Build site
  run: zensical build
```

## 迁移检查清单

使用此检查清单确保迁移完整：

- [ ] 安装 Zensical
- [ ] 配置文件准备（保留 mkdocs.yml 或转换为 zensical.toml）
- [ ] 选择主题变体（classic 或 modern）
- [ ] 本地测试（`zensical serve`）
- [ ] 检查所有页面和功能
- [ ] 更新部署脚本/CI/CD
- [ ] 构建网站（`zensical build`）
- [ ] 部署到生产环境
- [ ] 验证生产网站

## 逐步迁移策略

如果你有大型项目，可以采用逐步迁移策略：

### 阶段 1：并行运行

1. 安装 Zensical
2. 保留 `mkdocs.yml`
3. 使用 `zensical serve` 测试
4. 保持 MkDocs 作为备份

### 阶段 2：功能验证

1. 测试所有页面
2. 验证插件功能
3. 检查自定义样式
4. 测试部署流程

### 阶段 3：完全切换

1. 更新 CI/CD 配置
2. 切换到 Zensical 部署
3. （可选）转换为 zensical.toml
4. 移除 MkDocs 依赖

## 获取帮助

如果在迁移过程中遇到问题：

1. **查看文档** - [Zensical 官方文档](https://zensical.org/docs/)
2. **检查 FAQ** - [常见问题解答](faq.md)
3. **社区支持** - [Zensical-Wcowin 社区](https://support.qq.com/products/646913/)
4. **GitHub Issues** - [提交问题](https://github.com/Wcowin/Zensical-Wcowin/issues)

## 下一步

迁移完成后，探索 Zensical 的新功能：

- [即时导航配置](theme-customization.md#即时导航)
- [Modern 主题定制](theme-customization.md#modern-主题)
- [博客系统完全指南](blog-tutorial.md)
- [性能优化技巧](advanced/performance.md)

---

**参考资料**：

- [Zensical 官方文档 - Basics](https://zensical.org/docs/setup/basics/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)

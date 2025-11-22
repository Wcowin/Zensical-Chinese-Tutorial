---
hide:
  - navigation
  - toc
  - footer
comments: false
---

<center><font class="custom-font ml3">最好的 Zensical 中文教程</font></center>

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
    
    ![Zensical Logo](https://zensical.org/assets/images/logo.svg){ align=right width="200" style="border-radius: 15px;" }
    
    - [x] {==MkDocs 已停止更新==}，Zensical 是官方推荐的新一代
    - [x] {++即时导航++}，无需刷新页面
    - [x] {~~博客系统~~}，开箱即用
    - [x] 性能优异，加载迅速
    - [x] 𝕙𝕒𝕧𝕖 𝕒 𝕘𝕠𝕠𝕕 𝕥𝕚𝕞𝕖 !
    
    === "Mac/PC端"
        请在上方标签选择分类/左侧目录选择文章
    
    === "移动端"
        请点击左上角图标选择分类和文章

</div>

> 不同于市面上过时的 MkDocs 教程，本站提供了 **最详细、最便捷、最前沿** 的 Zensical 中文教程，与 [官方发布](https://zensical.org/about/roadmap/) 的版本同步。包含了 Zensical 的安装、配置、主题美化、博客系统等内容。无论你是初学者还是有经验的用户，都能在这里找到你需要的帮助。𝓳𝓾𝓼𝓽 𝓮𝓷𝓳𝓸𝔂 𝓲𝓽～

---

<div class="grid cards" markdown>

-   :simple-zenn:{ .lg .middle } __Zensical 快速开始（必看）__

    ---
    
    - [5 分钟快速开始](quick-start.md)
    - [Zensical 博客系统完全指南](blog-tutorial.md)
    - [zensical.toml 配置详解](configuration.md)
    - [从 MkDocs 迁移到 Zensical](migration.md)
    - [常见问题解答](faq.md)

-   :material-palette:{ .lg .middle } __主题定制__

    ---
    
    - [主题配置指南](theme-customization.md)
    - [自定义 CSS 样式](custom-css.md)
    - [自定义 JavaScript](custom-js.md)
    - [模板覆盖技巧](template-overrides.md)

-   :material-puzzle:{ .lg .middle } __插件系统__

    ---
    
    - [博客插件详解](plugins/blog.md)
    - [搜索插件配置](plugins/search.md)
    - [标签插件使用](plugins/tags.md)
    - [RSS 插件配置](plugins/rss.md)

-   :material-rocket:{ .lg .middle } __部署指南__

    ---
    
    - [Netlify 部署（推荐）](deployment/netlify.md)
    - [GitHub Pages 部署](deployment/github-pages.md)
    - [自托管部署](deployment/self-hosted.md)
    - [CI/CD 自动化](deployment/cicd.md)

-   :simple-aboutdotme:{ .lg .middle } __关于__

    ---
    
    - [Zensical-Wcowin 社区](https://support.qq.com/products/646913/){target="_blank"}
    - [留言板](feedback.md)
    - [案例展示](showcase.md)
    - [:octicons-arrow-right-24: 了解作者](about.md)
    - [请作者喝杯咖啡](sponsor.md)

</div>

## 🆚 Zensical vs MkDocs

| 特性 | Zensical | MkDocs |
|------|----------|--------|
| **维护状态** | ✅ 积极开发 | ⚠️ 已停止更新 |
| **即时导航** | ✅ 原生支持 | ❌ 需要插件 |
| **博客系统** | ✅ 开箱即用 | ⚠️ 需要插件 |
| **性能** | ✅ 优异 | ⚠️ 一般 |
| **现代化** | ✅ 现代设计 | ⚠️ 传统设计 |
| **配置文件** | TOML | YAML |
| **中文支持** | ✅ 完整 | ✅ 完整 |

## 📚 推荐学习路径

### 初学者路线

1. **第一步**：阅读 [5 分钟快速开始](quick-start.md)
2. **第二步**：学习 [zensical.toml 配置详解](configuration.md)
3. **第三步**：掌握 [博客系统完全指南](blog-tutorial.md)
4. **第四步**：尝试 [主题定制](theme-customization.md)
5. **第五步**：部署到线上 [Netlify 部署](deployment/netlify.md)

### 从 MkDocs 迁移

1. **第一步**：阅读 [从 MkDocs 迁移到 Zensical](migration.md)
2. **第二步**：了解 [配置文件差异](configuration.md#从-mkdocs-迁移)
3. **第三步**：处理 [插件兼容性](plugins/compatibility.md)
4. **第四步**：测试和调整
5. **第五步**：重新部署

### 高级用户路线

1. **模板系统**：学习 [模板覆盖技巧](template-overrides.md)
2. **性能优化**：阅读 [性能优化指南](advanced/performance.md)
3. **自动化**：配置 [CI/CD 自动化](deployment/cicd.md)
4. **扩展开发**：等待 Zensical 模块系统发布

## 🎯 核心特性

### 即时导航

Zensical 的即时导航功能让你的网站像单页应用一样流畅：

```toml
[project.theme]
features = [
    "navigation.instant",      # 即时导航
    "navigation.instant.prefetch",  # 预加载
]
```

### 博客系统

内置的博客系统，无需额外插件：

```toml
[project.plugins.blog]
post_date_format = "full"
draft = true
post_readtime = true
post_readtime_words_per_minute = 265
```

### Modern 主题

全新的 Modern 主题变体，更现代、更美观：

```toml
[project.theme]
variant = "modern"  # 或 "classic"
```

## 🚀 快速开始

```bash
# 安装 Zensical
pip install zensical

# 创建新项目
zensical new my-blog
cd my-blog

# 启动开发服务器
zensical serve
```

打开浏览器访问 `http://127.0.0.1:8000`

## 📖 文档结构

```
Zensical-Wcowin/
├── docs/
│   ├── index.md                    # 本页面
│   ├── quick-start.md              # 快速开始
│   ├── blog-tutorial.md            # 博客教程
│   ├── configuration.md            # 配置详解
│   ├── migration.md                # 迁移指南
│   ├── faq.md                      # 常见问题
│   ├── theme-customization.md      # 主题定制
│   ├── plugins/                    # 插件文档
│   ├── deployment/                 # 部署指南
│   └── advanced/                   # 高级主题
├── zensical.toml                   # 配置文件
└── README.md                       # 项目说明
```

## 💡 实用技巧

!!! tip "提示"
    - 使用 `zensical serve` 实时预览
    - 使用 `zensical build --clean` 清理构建
    - 查看 [官方文档](https://zensical.org/docs/) 获取最新信息

!!! warning "注意"
    Zensical 不支持 MkDocs hooks，请使用模板覆盖或 JavaScript 替代

!!! info "信息"
    本教程持续更新，与 Zensical 官方版本同步

## 🌟 案例展示

- [Wcowin 的博客](https://wcowin.work) - 使用 Zensical 构建
- [更多案例](showcase.md) - 查看更多精彩案例

## 🤝 参与贡献

欢迎参与 Zensical-Wcowin 的完善：

1. Fork 本仓库
2. 创建你的特性分支
3. 提交你的修改
4. 推送到分支
5. 创建 Pull Request

## 📞 联系方式

- **GitHub**: [Wcowin/Zensical-Wcowin](https://github.com/Wcowin/Zensical-Wcowin)
- **Email**: wcowin@qq.com
- **微信**: 扫描下方二维码

---

<center>
**开始你的 Zensical 之旅吧！** 🚀
</center>

<style>
body::before {
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
  top: 0;
  transform-style: flat;
  pointer-events: none;
  z-index: -1;
}

@media (max-width: 768px) {
  body::before {
    display: none;
  }
}
</style>

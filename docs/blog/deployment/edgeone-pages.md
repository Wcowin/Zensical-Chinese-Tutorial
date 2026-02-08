---
title: 使用 EdgeOne Pages 托管 Zensical 站点
date: 2026-02-08
authors:
  - name: Luwei
    email: yang92636@qq.com
categories:
  - 部署指南
---

# 使用 EdgeOne Pages 托管 Zensical 站点

> 使用 EdgeOne Pages 部署 Zensical 网站，免费！在拥有备案域名的前提下，国内访问速度快。

## 关于 EdgeOne Pages

**EdgeOne Pages** 是腾讯云基于 EdgeOne 基础设施打造的边缘无服务器开发部署平台。它不仅提供从前端页面到动态 API 的全栈部署体验，更重要的是，它利用边缘网络进行全球加速，非常适合构建博客、营销网站、文档站点等现代 Web 项目。

### 🌏 关键注意事项：区域选择

在创建项目前，请务必根据你的**域名备案情况**选择加速区域，这是最关键的一步：

> **如果你拥有国内备案域名**：
> 强烈建议选择 **中国大陆** 或 **全球可用区**。将站点托管在 EdgeOne 国内的 CDN 节点上，国内用户将获得极致的访问速度和丝滑体验。

> **如果你没有国内备案域名**：
> 创建项目时**必须**选择加速区域为：**全球可用区（不含中国大陆）**。
> 
> *注意：如果选错区域，后续将无法绑定未备案的个人域名。且加速区域一旦选定，无法修改（只能删除项目重建）。*

![选择加速区域示意图](https://s1.imagehub.cc/images/2026/02/07/d2f7cae1d337fcff767a6f59de955ce5.png)

## 准备工作

在开始部署之前，请确保你已完成以下准备：

- [x] **注册腾讯云账号**：并已开通 [EdgeOne Pages](https://console.cloud.tencent.com/edgeone/pages) 服务。

- [x] **准备 Zensical 项目**：本地已有一个可运行的 Zensical 站点（或新建一个）。
- [x] **Github 仓库**：将你的项目代码托管在 Github 上。

## 方案选择：哪种方式适合你？

本文提供两种部署方案，请根据需求选择：

1. **原生构建（推荐）**：通过 edgeone.json 配置，直接在 EdgeOne 服务器上安装 Python 依赖并构建。
    - *优点*：配置简单，无需配置 Github Actions，代码推送即部署。
    - *缺点*：依赖 EdgeOne 环境。
2. **Github Actions 构建**：在 Github 上构建完成后，仅将静态文件推送到 EdgeOne。
    - *优点*：环境完全可控，构建速度快，EdgeOne 仅作为静态文件托管。
    - *缺点*：需要配置 Workflow 文件，仓库会多一个分支。

## 方法一：通过 edgeone.json 进行部署

EdgeOne Pages 的原生环境主要面向 Node.js，虽然官方未列出对 Python 的支持，但经实测其环境中包含 Python 解释器。我们可以通过自定义脚本“曲线救国”。

### 1. 准备`get-pip.py` 文件

由于 EdgeOne 环境中只有 Python 而没有 pip 包管理器，我们需要手动安装它。
在你的项目根目录终端执行以下命令，下载安装脚本：

```bash
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
```

执行后，请确认项目根目录下生成了 `get-pip.py` 文件。

### 2. 配置 `pcakage.json`

EdgeOne Pages 构建系统会优先检测 package.json。虽然我们是 Python 项目，但也**必须**欺骗构建系统，让它认为这是一个合法的项目。

在根目录新建 package.json，内容填入空的 JSON 对象即可：

```json
{}
```

**⚠️ 警告**：如果缺少此文件，EdgeOne 可能会在构建初始化阶段报错，导致部署失败。
![image-20260106214423262](https://s1.imagehub.cc/images/2026/02/07/94f2d4eff344eb3877a9a267c1155fd1.png)

### 3. 创建核心配置文件 `edgeone.json`

在项目根目录创建 edgeone.json。这个文件告诉 EdgeOne 如何配置环境、构建网站以及发布哪个目录。

请写入以下内容：

```json
{
  "installCommand": "python3 get-pip.py && python3 -m pip install zensical --upgrade pip",
  "buildCommand": "python3 -m zensical build --clean",
  "outputDirectory": "./site",
  "headers": [
    {
      "source": "/*",
      "headers": [
        {
          "key": "X-Frame-Options",
          "value": "DENY"
        },
        {
          "key": "Cache-Control",
          "value": "max-age=7200"
        }
      ]
    }
  ]
}
```

**配置详解：**

- **installCommand (环境安装)**:python3 get-pip.py: 运行下载的脚本，安装 pip。python3 -m pip install ...: 升级 pip 并安装 zensical 库。使用 python3 -m 是为了确保调用的是当前环境下的解释器。
- **buildCommand (构建指令)**:python3 -m zensical build --clean: 调用 Zensical 生成静态网页，--clean 确保每次构建前清理旧缓存，防止样式混乱。
- **outputDirectory (输出目录)**:./site: Zensical 默认的生成目录。EdgeOne 会将此目录发布到外网。
- **headers (可选优化)**:配置 HTTP 响应头，增加安全性（防止点击劫持）并设置缓存策略（2小时缓存），提升访问体验。

更多细节配置详见[官方文档]([edgeone.json](https://edgeone.cloud.tencent.com/pages/document/162936771610066944))。

### 4. 推送并部署

1. 将包含 edgeone.json、package.json、get-pip.py 的代码推送到 Github。
2. 进入 [EdgeOne 控制台](https://console.cloud.tencent.com/edgeone/pages)，点击 **新建项目**。
3. 选择 **导入 Git 仓库**，授权并选中你的 Zensical 项目。
4. **构建配置**：由于我们有了 edgeone.json，控制台里的配置会被自动覆盖，直接点击部署即可。

等待约 1-3 分钟，构建成功后你将获得一个临时访问域名，此时即可绑定你自己的域名。

## 方法二：通过 Gihub Action 进行部署

如果你希望构建过程更可控，或者 EdgeOne 的环境未来发生变化导致方法一失效，使用 Github Actions 是更稳健的选择。

### 1. 配置 Workflow

在项目根目录创建 `.github/workflows/deploy.yml` 文件：

```yaml
name: Build and Deploy Zensical to Deploy Branch

# 触发条件：当推送到 main 分支时运行 (如果你的主分支叫 master，请修改此处)
on:
  push:
    branches:
      - main
  # 允许在 Actions 页面手动触发
  workflow_dispatch:

# 设置权限，允许 GITHUB_TOKEN 推送代码到分支
permissions:
  contents: write

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
      # 1. 检出代码
      - name: Checkout repository
        uses: actions/checkout@v4

      # 2. 设置 Python 环境
      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.10' # 根据需要修改 Python 版本

      # 3. 安装依赖并构建
      - name: Install and Build
        run: |
          pip install zensical
          zensical build --clean

      # 4. 部署 'site' 文件夹到 'deploy' 分支
      - name: Deploy to deploy branch
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          branch: deploy   # 目标分支，部署后提交到那个分支
          folder: site     # 构建生成的输出文件夹，存放build后产物的目录
          clean: true      # 部署前清空目标分支的旧文件
          commit-message: "Deploy: ${{ github.event.head_commit.message }}" # 自定义提交信息
          single-commit: true # 使用单次提交，保持分支整洁
```

### 2. EdgeOne 设置

1. 等待 Github Action 运行完毕，你的仓库会自动多出一个 deploy 分支。
2. 进入 [EdgeOne 控制台](https://console.cloud.tencent.com/edgeone/pages) 创建项目。
3. 在配置界面中，**生产分支 (Production Branch)** 选择 deploy。
4. 构建设置：保持默认设置，即框架预设为 Other，根目录为 `./`（因为 deploy 分支里已经是纯 HTML 文件了）。

## 总结

EdgeOne Pages 结合国内 CDN 节点，为 Zensical 站点提供了极佳的访问速度。

- 如果你追求配置简单，且项目依赖较少，方法一（edgeone.json）是最快捷的路径。
- 如果你追求构建稳定性和环境可控，方法二（Github Actions）是通用的最佳实践。

祝你的 Zensical 站点部署顺利！🚀

## 番外：一个尝试失败的方案

在探索 EdgeOne Pages 的部署方式时，我曾尝试利用 EdgeOne 提供的 GitHub Action 工作流，旨在实现项目的自动构建和部署。然而，在实践过程中，这个方案遇到了一些挑战。

### 部署工作流卡顿问题

笔者参考了 [EdgeOne Pages 官方文档中关于 GitHub Action 的指南](https://edgeone.cloud.tencent.com/pages/document/180252837825597440) 编写了部署工作流。但在实际执行时，工作流在以下特定任务步骤中出现了长时间卡顿，未能成功完成部署：

```yaml
- name: Deploy to EdgeOne Pages
  run: npx edgeone pages deploy <outputDirectory> -n <projectName> -t ${{ secrets.EDGEONE_API_TOKEN }} [-e <env>]
  env:
    EDGEONE_API_TOKEN: ${{ secrets.EDGEONE_API_TOKEN }}
```

该任务旨在通过 `npx edgeone pages deploy` 命令将构建产物部署到 EdgeOne Pages。尽管配置了 `EDGEONE_API_TOKEN`，但该步骤未能正常推进。

> 感兴趣的读者可以自行尝试，但请务必注意以下几点。

### 部署实践中的重要坑点与建议

通过这次尝试，笔者总结了一些关于使用 GitHub Action 部署 EdgeOne Pages 的关键注意事项：

1.  **项目创建与加速区域默认值**：
    *   EdgeOne 官方确实支持通过 `EDGEONE_API_TOKEN` 来创建新的 Pages 项目。
    *   **⚠️ 致命点**：如果你的 Pages 项目是**由 GitHub Action 自动创建**的（即在控制台没有预先创建），那么它默认的加速区域会被设置为**“全球可用区（包含中国大陆）”**。
    *   **后果**：在这种默认设置下，你将**无法绑定未备案的域名**。
    *   **强烈建议**：为了确保能够选择合适的加速区域（特别是对于无备案域名用户需要选择**“全球可用区（不含中国大陆）”**），**请务必在 EdgeOne 控制台手动创建 Pages 项目（通过*直接上传*选项创建项目）并配置好加速区域，然后再将 GitHub Action 配置为部署到已存在的项目。**
2.  **工作流卡死与资源消耗**：
    *   GitHub Actions 工作流一旦出现卡死现象，会持续占用 GitHub 的 CI/CD 资源。
    *   **⚠️ 警告**：请务必及时手动取消这些卡顿的工作流。长时间不取消，可能会导致 GitHub 账号的 Actions 分钟数被大量消耗，甚至可能面临使用限制或封号风险。

## 下一步

- 访问 [EdgeOne 控制台](https://console.cloud.tencent.com/edgeone/pages)
- 查看 [EdgeOne Pages 文档](https://edgeone.cloud.tencent.com/pages/document/162936635171454976)

---

**参考资料**：  

- [EdgeOne Pages 官方文档](https://edgeone.cloud.tencent.com/pages/document/162936635171454976)
- [Zensical 官方文档](https://zensical.org/docs/)

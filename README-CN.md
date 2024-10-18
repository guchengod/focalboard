> [!WARNING]
> 此仓库目前无人维护。如果您有兴趣成为维护者，请 [点击这里联系我们](https://github.com/mattermost-community/focalboard/issues/5038)。
>
> 该仓库仅包含独立版 Focalboard。如果您正在寻找 Mattermost 插件，请参见 [mattermost/mattermost-plugin-boards](https://github.com/mattermost/mattermost-plugin-boards)。
>
> 我对 Focalboard 项目有浓厚的兴趣，并且愿意投入时间和精力继续维护和改进该项目。Focalboard 作为一个优秀的开源项目管理工具，在促进个人和团队的工作管理中起到了重要作用。我计划通过定期修复问题、优化功能，确保该项目能够持续为用户带来价值。

# Focalboard

![CI 状态](https://github.com/mattermost/focalboard/actions/workflows/ci.yml/badge.svg)
![CodeQL](https://github.com/mattermost/focalboard/actions/workflows/codeql-analysis.yml/badge.svg)
![开发发布](https://github.com/mattermost/focalboard/actions/workflows/dev-release.yml/badge.svg)
![生产发布](https://github.com/mattermost/focalboard/actions/workflows/prod-release.yml/badge.svg)

![Focalboard](website/site/static/img/hero.jpg)

Focalboard 是一个开源的、多语言的、自托管的项目管理工具，是 Trello、Notion 和 Asana 的替代方案。

它可以帮助个人和团队定义、组织、跟踪和管理工作。Focalboard 有两个版本：

* **[个人桌面版](https://www.focalboard.com/docs/personal-edition/desktop/)**：一个独立的单用户 [macOS](https://apps.apple.com/app/apple-store/id1556908618?pt=2114704&ct=website&mt=8)、[Windows](https://www.microsoft.com/store/apps/9NLN2T0SX9VF?cid=website) 或 [Linux](https://www.focalboard.com/download/personal-edition/desktop/#linux-desktop) 桌面应用，用于个人待办事项和项目管理。

* **[个人服务器版](https://www.focalboard.com/download/personal-edition/ubuntu/)**：一个独立的多用户服务器，适合开发和个人使用。

## 试用 Focalboard

### 个人桌面版 (Windows, Mac 或 Linux 桌面)

* **Windows**：从 [Windows 应用商店](https://www.microsoft.com/store/productId/9NLN2T0SX9VF) 下载，或从 [最新发布](https://github.com/mattermost/focalboard/releases) 下载 `focalboard-win.zip`，解压并运行 `Focalboard.exe`。
* **Mac**：从 [Mac 应用商店](https://apps.apple.com/us/app/focalboard-insiders/id1556908618?mt=12) 下载。
* **Linux 桌面**：从 [最新发布](https://github.com/mattermost/focalboard/releases) 下载 `focalboard-linux.tar.gz`，解压并运行 `focalboard-app`。

### 个人服务器版

**Ubuntu**：您可以下载并运行编译好的 Focalboard **个人服务器版**，请按照 [我们的最新安装指南](https://www.focalboard.com/download/personal-edition/ubuntu/) 操作。

### API 文档

Boards API 文档可在此处找到：<https://htmlpreview.github.io/?https://github.com/mattermost/focalboard/blob/main/server/swagger/docs/html/index.html>

### 开始使用

我们的 [开发者指南](https://developers.mattermost.com/contribute/focalboard/personal-server-setup-guide) 提供了详细的说明，帮助您设置 **个人服务器版** 的开发环境。您还可以加入 [~Focalboard 社区频道](https://community.mattermost.com/core/channels/focalboard)，与其他开发者交流。

在 focalboard 目录下创建一个 `.env` 文件，内容如下：

```
EXCLUDE_ENTERPRISE="1"
```

构建服务器：

```
make prebuild
make
```

运行服务器：

```
 ./bin/focalboard-server
```

然后在浏览器中打开 [`http://localhost:8000`](http://localhost:8000) 访问您的 Focalboard 服务器。端口配置在 `config.json` 文件中。

一旦服务器运行起来，您可以通过在另一个终端窗口中运行 `make webapp` 来重新构建 web 应用。重新加载浏览器以查看更改。

### 构建和运行独立桌面应用

您可以构建包含本地运行的 SQLite 服务器的独立应用：

* **Windows**：
    * *需要 Windows 10，[Windows 10 SDK](https://developer.microsoft.com/en-us/windows/downloads/sdk-archive/) 10.0.19041.0 和 .NET 4.8 开发包*
    * 打开一个 `git-bash` 提示符。
    * 运行 `make prebuild`
    * 上述预构建步骤仅在您更改或想要安装 npm 依赖项等时运行。
    * 一旦预构建完成，您可以重复以下步骤来构建应用并查看更改。
    * 运行 `make win-wpf-app`
    * 运行 `cd win-wpf/msix && focalboard.exe`
* **Mac**：
    * *需要 macOS 11.3+ 和 Xcode 13.2.1+*
    * 运行 `make prebuild`
    * 上述预构建步骤仅在您更改或想要安装 npm 依赖项等时运行。
    * 一旦预构建完成，您可以重复以下步骤来构建应用并查看更改。
    * 运行 `make mac-app`
    * 运行 `open mac/dist/Focalboard.app`
* **Linux**：
    * *在 Ubuntu 18.04 上测试*
    * 安装 `webgtk` 依赖
        * 运行 `sudo apt-get install libgtk-3-dev`
        * 运行 `sudo apt-get install libwebkit2gtk-4.0-dev`
    * 运行 `make prebuild`
    * 上述预构建步骤仅在您更改或想要安装 npm 依赖项等时运行。
    * 一旦预构建完成，您可以重复以下步骤来构建应用并查看更改。
    * 运行 `make linux-app`
    * 解压 `linux/dist/focalboard-linux.tar.gz` 到您选择的目录
    * 从您选择的目录运行 `focalboard-app`
* **Docker**：
    * 从官方镜像本地运行：
        * `docker run -it -p 80:8000 mattermost/focalboard`
    * 为当前架构构建：
        * `docker build -f docker/Dockerfile .`
    * 为自定义架构构建（实验性）：
        * `docker build -f docker/Dockerfile --platform linux/arm64 .`

目前跨平台编译尚未完全支持，因此请在相应的平台上构建。有关每个平台的详细步骤，请参考 GitHub Actions 工作流（`build-mac.yml`，`build-win.yml`，`build-ubuntu.yml`）。

### 单元测试

在提交代码之前，运行 `make ci`，这与 `.gitlab-ci.yml` 工作流类似，包括：

* **服务器单元测试**：`make server-test`
* **Web 应用 ESLint**：`cd webapp; npm run check`
* **Web 应用单元测试**：`cd webapp; npm run test`
* **Web 应用 UI 测试**：`cd webapp; npm run cypress:ci`

### 保持更新

* **更新**：请参阅 [更新日志](CHANGELOG.md) 了解最新更新
* **Bug 报告**：[提交 Bug 报告](https://github.com/mattermost/focalboard/issues/new?assignees=&labels=bug&template=bug_report.md&title=)
* **聊天**：加入 [~Focalboard 社区频道](https://community.mattermost.com/core/channels/focalboard)

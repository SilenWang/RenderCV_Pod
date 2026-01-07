# RenderCV Pod

[English](README.md) | 中文

## 为什么有这个项目

虽然 RenderCV 提供了官方Web App，但作为程序员，我更倾向于在熟悉的开发环境中使用，毕竟RenderCV 提供了功能强大的命令行界面（CLI），这种方式更加简单直接并高效。

本项目提供了一个预配置的开发容器（Dev Container），集成了 RenderCV 及其所有依赖，让你可以立即开始在 VSCode 中编写和生成专业的简历，无需在本地安装任何软件。

## 容器内的工具

这个开发容器基于 Ubuntu 构建，并包含以下组件：

1. **Pixi 包管理器**：预装了最新版本的 Pixi（v0.62.2），用于管理项目依赖
2. **Python 3.12**：通过 Pixi 安装的 Python 3.12 运行时
3. **RenderCV**：通过 Pixi 安装的 RenderCV Python 包，包含所有额外功能（full extra）
4. **Visual Studio Code 扩展**：预装了以下扩展：
   - `naumovs.color-highlight`：颜色高亮
   - `tamasfe.even-better-toml`：TOML 文件支持
   - `adamraichu.pdf-viewer`：PDF 预览增强
   - `redhat.vscode-yaml`：YAML 语言支持
5. Aider: 终端中运行的AI编码工具

容器配置位于 `.devcontainer/` 目录中：
- `Dockerfile`：定义了容器镜像的构建步骤，主要安装 Pixi 包管理器
- `devcontainer.json`：配置 VSCode 开发容器的设置，包括主题和扩展

## 使用方法

### 启动容器

-  使用 Devpod: `devpod up https://github.com/SilenWang/RenderCV_Pod`
-  使用 Github Codespace: 从这个项目启动一个 Codespace

### 编辑配置

可以参照 [RenderCV 官方文档](https://docs.rendercv.com/) 来创建和编辑配置文件

### 在Aider辅助下编辑配置

- 根据 [aider 的文档](https://aider.chat/docs/llms.html) 设置语言模型Key
- 运行 `pixi run aider sample.yaml`, 让Aider帮你编辑配置

### 生成简历

运行 `pixi run cv sample.yaml`, 简历将生成在 `rendercv_output` 文件夹
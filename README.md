# RenderCV Pod

<div align="center">
  <a href="#中文">中文</a> | <a href="#english">English</a>
</div>

<a id="中文"></a>

## 为什么选择这个项目

虽然 RenderCV 提供了官方桌面应用程序，但作为程序员，我们更倾向于在熟悉的开发环境中工作。RenderCV 提供了功能强大的命令行界面（CLI），直接在 Visual Studio Code 中进行编辑和预览，并使用 RenderCV CLI 生成简历，这种方式更加简单直接、高效可控。

本项目提供了一个预配置的开发容器（Dev Container），集成了 RenderCV 及其所有依赖，让你可以立即开始在 VSCode 中编写和生成专业的简历文档，无需在本地安装任何软件。

## 容器包含的内容

这个开发容器基于 Ubuntu 构建，并包含以下组件：

1. **基础环境**：基于 `mcr.microsoft.com/devcontainers/base:ubuntu` 镜像，提供稳定的 Linux 环境
2. **Pixi 包管理器**：预装了最新版本的 Pixi（v0.62.2），用于管理项目依赖
3. **Python 3.12**：通过 Pixi 安装的 Python 3.12 运行时
4. **RenderCV**：通过 Pixi 安装的 RenderCV Python 包，包含所有额外功能（full extra）
5. **Rust 工具链**：通过 Pixi 安装的 Rust，用于可能的扩展开发
6. **Visual Studio Code 扩展**：预装了以下扩展：
   - `naumovs.color-highlight`：颜色高亮
   - `tamasfe.even-better-toml`：TOML 文件支持
   - `wytheglobal.pdfmore`：PDF 预览增强
   - `redhat.vscode-yaml`：YAML 语言支持

容器配置位于 `.devcontainer/` 目录中：
- `Dockerfile`：定义了容器镜像的构建步骤，主要安装 Pixi 包管理器
- `devcontainer.json`：配置 VSCode 开发容器的设置，包括主题和扩展

项目使用 Pixi 作为包管理器（见 `pixi.toml`），管理以下依赖：
- Python 3.12.*
- Rust
- RenderCV（通过 PyPI 安装，包含完整功能）
- 其他 Python 包：setuptools, aider-chat

**注意**：要使用 RenderCV 生成 PDF，你需要在容器内额外安装 LaTeX 发行版（如 texlive-full）。可以在 Dockerfile 中添加相应的安装命令，或进入容器后手动安装。

## 使用方法

### 前提条件
- 安装 [Docker](https://www.docker.com/products/docker-desktop/)
- 安装 [Visual Studio Code](https://code.visualstudio.com/)
- 安装 VSCode 的 [Dev Containers 扩展](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### 快速开始
1. 在 VSCode 中打开本项目文件夹
2. 按下 `F1` 键，输入并选择 **"Dev Containers: Reopen in Container"**
3. 等待容器构建完成（首次运行可能需要几分钟以下载基础镜像和安装依赖）
4. 容器启动后，会自动运行 `pixi install -a` 安装所有依赖（通过 `postCreateCommand` 配置）
5. 容器准备就绪后，你可以在集成终端中直接使用 `rendercv` 命令

### 创建和编辑简历
1. 在项目根目录创建或编辑 `resume.yaml` 文件（可以参考 RenderCV 的示例模板）
2. 使用以下命令预览简历：
   ```bash
   rendercv preview resume.yaml
   ```
3. 生成最终的 PDF 文档（需要先安装 LaTeX）：
   ```bash
   rendercv render resume.yaml
   ```
4. 生成的 PDF 将保存在当前目录，文件名为 `resume.pdf`

### 安装 LaTeX（必需）
由于基础镜像未包含 LaTeX，你需要手动安装才能生成 PDF：
```bash
sudo apt-get update && sudo apt-get install -y texlive-full
```
或者，你可以修改 `.devcontainer/Dockerfile`，在构建时自动安装 LaTeX。

### 使用 Pixi 管理环境
本项目使用 Pixi 来管理 Python 和 RenderCV 的版本。常用命令：
- 安装依赖：`pixi install`
- 运行 rendercv：`pixi run rendercv --help`
- 使用预定义任务：`pixi run cv your_resume.yaml`（根据 pixi.toml 中的配置）
- 更新依赖：`pixi update`

### 自定义配置
- 修改 `.devcontainer/devcontainer.json` 来调整 VSCode 设置或安装额外的扩展
- 编辑 `.devcontainer/Dockerfile` 来添加系统包（如 LaTeX）或更改基础镜像
- 更新 `pixi.toml` 来调整 Python 版本或添加新的依赖

### 许可证
本项目基于 MIT 许可证开源，详见 [LICENSE](LICENSE) 文件。

---

<a id="english"></a>
## Why this project

Although RenderCV provides an official desktop application, as programmers we prefer to work in familiar development environments. RenderCV offers a powerful command-line interface (CLI) that allows you to edit and preview directly in Visual Studio Code, and generate resumes using the RenderCV CLI. This approach is more straightforward, efficient, and controllable.

This project provides a pre-configured development container (Dev Container) that integrates RenderCV and all its dependencies, enabling you to immediately start writing and generating professional resume documents in VSCode without installing any software locally.

## What is in this container

This development container is built on Ubuntu and includes the following components:

1. **Base Environment**: Based on the `mcr.microsoft.com/devcontainers/base:ubuntu` image, providing a stable Linux environment
2. **Pixi Package Manager**: Pre-installed with the latest version of Pixi (v0.62.2) for managing project dependencies
3. **Python 3.12**: Python 3.12 runtime installed via Pixi
4. **RenderCV**: RenderCV Python package installed via Pixi, including all extra features (full extra)
5. **Rust Toolchain**: Rust installed via Pixi for potential extension development
6. **Visual Studio Code Extensions**: Pre-installed extensions:
   - `naumovs.color-highlight`: Color highlighting
   - `tamasfe.even-better-toml`: TOML file support
   - `wytheglobal.pdfmore`: PDF preview enhancement
   - `redhat.vscode-yaml`: YAML language support

Container configuration is located in the `.devcontainer/` directory:
- `Dockerfile`: Defines the container image build steps, primarily installing the Pixi package manager
- `devcontainer.json`: Configures VSCode development container settings, including themes and extensions

The project uses Pixi as a package manager (see `pixi.toml`) to manage the following dependencies:
- Python 3.12.*
- Rust
- RenderCV (installed via PyPI with full functionality)
- Other Python packages: setuptools, aider-chat

**Note**: To use RenderCV to generate PDFs, you need to additionally install a LaTeX distribution (e.g., texlive-full) inside the container. You can add the corresponding installation command to the Dockerfile or install it manually after entering the container.

## How to use

### Prerequisites
- Install [Docker](https://www.docker.com/products/docker-desktop/)
- Install [Visual Studio Code](https://code.visualstudio.com/)
- Install the [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers) for VSCode

### Quick Start
1. Open this project folder in VSCode
2. Press `F1`, type and select **"Dev Containers: Reopen in Container"**
3. Wait for the container to build (the first run may take several minutes to download the base image and install dependencies)
4. After the container starts, it will automatically run `pixi install -a` to install all dependencies (via the `postCreateCommand` configuration)
5. Once the container is ready, you can directly use the `rendercv` command in the integrated terminal

### Create and Edit Resumes
1. Create or edit a `resume.yaml` file in the project root directory (you can refer to RenderCV's example templates)
2. Preview the resume using:
   ```bash
   rendercv preview resume.yaml
   ```
3. Generate the final PDF document (requires LaTeX to be installed first):
   ```bash
   rendercv render resume.yaml
   ```
4. The generated PDF will be saved in the current directory with the filename `resume.pdf`

### Install LaTeX (Required)
Since the base image does not include LaTeX, you need to install it manually to generate PDFs:
```bash
sudo apt-get update && sudo apt-get install -y texlive-full
```
Alternatively, you can modify `.devcontainer/Dockerfile` to automatically install LaTeX during build.

### Using Pixi to Manage the Environment
This project uses Pixi to manage Python and RenderCV versions. Common commands:
- Install dependencies: `pixi install`
- Run rendercv: `pixi run rendercv --help`
- Use predefined tasks: `pixi run cv your_resume.yaml` (according to the configuration in pixi.toml)
- Update dependencies: `pixi update`

### Custom Configuration
- Modify `.devcontainer/devcontainer.json` to adjust VSCode settings or install additional extensions
- Edit `.devcontainer/Dockerfile` to add system packages (such as LaTeX) or change the base image
- Update `pixi.toml` to adjust Python versions or add new dependencies

### License
This project is open source under the MIT License. See the [LICENSE](LICENSE) file for details.

---

<div align="center">
  <a href="#中文">中文</a> | <a href="#english">English</a>
</div>

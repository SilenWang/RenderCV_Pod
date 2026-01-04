# RenderCV Pod

English | [中文](README.zh.md)

## Why this project

Although RenderCV provides an official web app, as programmers, I prefer to work in familiar development environments. RenderCV already offers a powerful CLI, use it is more straightforward, and efficient.

This project provides a pre-configured development container (Dev Container) that integrates RenderCV and all its dependencies, enabling one to immediately start writing and generating professional resume documents in VSCode without installing any software locally.

## What is in this container

This development container is built on Ubuntu and includes the following components:

1. **Pixi Package Manager**: Pre-installed with the latest version of Pixi (v0.62.2) for managing project dependencies
2. **Python 3.12**: Python 3.12 runtime installed via Pixi
3. **RenderCV**: RenderCV Python package installed via Pixi, including all extra features (full extra)
4. **Visual Studio Code Extensions**: Pre-installed extensions:
   - `naumovs.color-highlight`: Color highlighting
   - `tamasfe.even-better-toml`: TOML file support
   - `adamraichu.pdf-viewer`: PDF preview enhancement
   - `redhat.vscode-yaml`: YAML language support
5. Aider: AI pair programming in your terminal

Container configuration is located in the `.devcontainer/` directory:
- `Dockerfile`: Defines the container image build steps, primarily installing the Pixi package manager
- `devcontainer.json`: Configures VSCode development container settings, including themes and extensions

## How to use

### Start the container

-  Using Devpod: `devpod up https://github.com/SilenWang/RenderCV_Pod`
-  Using Github Codespace: Start a codespace from this repo

### Create or edit your config file yourself

You can refer to [RenderCV Document](https://docs.rendercv.com/) to create and edit your config file

### Create or edit your config file using aider

- Set your LLM API KEY accoring to [aider document](https://aider.chat/docs/llms.html)
- Run `pixi run aider sample.yaml`, and ask aider to help you edit the config file

### Build your CV

Run `pixi run cv sample.yaml`, your CV will be in `rendercv_output` folder
一个基于多模态 AI 技术的智能助手，旨在提升企业办公自动化流程的效率。它能够处理语音、图像和文本等多种输入形式，通过精确的提示工程和强大的自然语言处理能力，为用户生成高质量的 PowerPoint 演示文稿。ChatPPT 不仅简化了信息收集和内容创作过程，还通过自动化的报告生成和分析功能，帮助企业快速、准确地完成各类汇报和展示任务，从而显著提升工作效率和业务价值。

### 主要功能

- **多模态输入支持**：支持语音、图像、文本等多种输入形式，灵活适应用户的使用需求。
- **自动生成演示文稿**：基于输入内容，自动生成结构化的 PowerPoint 演示文稿，支持多种布局和模板。
- **语音识别和文本转换**：自动将语音输入转化为文本，进行内容处理和文稿生成，降低用户的操作成本。
- **图像处理与嵌入**：支持将用户上传的图片自动嵌入演示文稿中，并根据内容智能选择合适的布局。
- **多语言支持**：结合 OpenAI 模型和其他语言模型，支持中英文等多语言的演示文稿生成和报告输出。
- **可视化界面**：通过 Gradio 实现简洁易用的图形化界面，让用户无需复杂配置即可快速生成演示文稿。

### 产品演示

https://github.com/user-attachments/assets/37d32bec-928e-4961-98b3-189ce15ead2e


**自动生成的演示文稿内容**

![chatppt_presentation_demo](images/chatppt_presentation_demo.png)

## 使用 Docker 部署服务

ChatPPT 提供了 Docker 支持，以便在隔离环境中运行。以下是使用 Docker 运行的步骤。

### 1. 运行 Docker 容器

使用以下命令运行 ChatPPT 指定版本（如:v0.7）Docker 容器服务。关于如何 [使用 Docker 构建与验证](#使用-docker-构建与验证)。

```sh
docker run -it -p 7860:7860 -e LANGCHAIN_API_KEY=$LANGCHAIN_API_KEY -e OPENAI_API_KEY=$OPENAI_API_KEY -v $(pwd)/outputs:/app/outputs chatppt:v0.7

```

### 2. 参数说明

在运行容器时，可以通过环境变量传入`LANGCHAIN_API_KEY` 和 `OPENAI_API_KEY`，例如：

```sh
-e LANGCHAIN_API_KEY=$LANGCHAIN_API_KEY -e OPENAI_API_KEY=$OPENAI_API_KEY 
```

将本地的 `outputs` 文件夹挂载到容器内的 `/app/outputs`，便于访问生成的文件。

```sh
-v $(pwd)/outputs:/app/outputs`
```



## 使用 Docker 构建与验证

为了便于在各种环境中构建和部署 ChatPPT 项目，我们提供了 Docker 支持。该支持包括以下文件和功能：

### 1. `Dockerfile`

#### 用途
`Dockerfile` 是用于定义 ChatPPT 项目 Docker 镜像构建过程的配置文件。它描述了构建步骤，包括安装依赖、复制项目文件、运行单元测试等。

#### 关键步骤
- 使用 `python:3.10-slim` 作为基础镜像，并设置工作目录为 `/app`。
- 复制项目的 `requirements.txt` 文件，并安装所有 Python 依赖。
- 复制项目的所有文件到容器中，并赋予 `validate_tests.sh` 脚本执行权限。
- 在构建过程中执行 `validate_tests.sh` 脚本，以确保所有单元测试通过。如果测试失败，构建过程将中止。
- 构建成功后，将默认运行 `src/main.py` 作为容器的入口

点，以启动 ChatPPT 服务。

### 2. `build_image.sh`

#### 用途
`build_image.sh` 是一个自动构建 Docker 镜像的 Shell 脚本。它从当前的 Git 分支中获取分支名称，并将其用作 Docker 镜像的标签，便于在不同开发分支上生成不同的 Docker 镜像。

#### 功能
- 获取当前 Git 分支名称，并将其用作 Docker 镜像的标签，以便追踪不同开发分支的版本。
- 使用 `docker build` 命令构建 Docker 镜像，并使用当前 Git 分支名称作为标签。

#### 使用示例
```bash
./build_image.sh
```

![build_docker_image](images/build_docker_image.png)

通过这些脚本和配置文件，ChatPPT 项目可以在不同的开发分支中确保构建的 Docker 镜像基于通过单元测试的代码，从而提高了代码质量和部署的可靠性。

### 贡献

我们欢迎所有的贡献！如果你有任何建议或功能请求，请先开启一个议题讨论。你的帮助将使 ChatPPT 变得更加完善。

### 许可证

该项目根据 **Apache 2.0** 许可证进行许可。详情请参见 [LICENSE](LICENSE) 文件。

### 联系

项目作者: Django Peng

项目链接: https://github.com/DjangoPeng/ChatPPT

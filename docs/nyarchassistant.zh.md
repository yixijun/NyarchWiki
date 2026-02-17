# Nyarch Assistant
<div style="text-align: center;">
<img src="https://raw.githubusercontent.com/NyarchLinux/NyarchAssistant/refs/heads/master/data/icons/hicolor/scalable/apps/moe.nyarchlinux.assistant.svg" alt="nyarchassistant" width="192" height="192"/>
</div>
<div style="text-align: center;">

Nyarch Assistant 是 Nyarch Linux 官方的 <b>AI 老婆助手</b>。
</div>

![screenshot](https://raw.githubusercontent.com/NyarchLinux/NyarchAssistant/refs/heads/master/screenshots/1b.png)

## Nyarch Assistant 和 Newelle

Nyarch Assistant 是 [Newelle](https://github.com/qwersyk/Newelle) 的一个分支。

**Newelle** 可在 [Flathub](https://flathub.org/apps/io.github.qwersyk.Newelle) 上获得，旨在成为**一般 Linux 用户的 AI 聊天机器人**，而 **Nyarch Assistant** 有一些**动漫和 Nyarch Linux 相关的内容**，对普通用户来说没有意义。

Newelle 和 Nyarch Linux 将**始终**保持彼此同步，Newelle 扩展将始终与 Nyarch Assistant 扩展兼容。

## 功能
- **您梦想中的老婆，听您指挥**：从庞大的 TTS 语音和 Live2D 或 LivePNG 模型库中选择，创建完美的虚拟伴侣。

- **终端命令执行**：直接通过 AI 执行终端命令。

- **高级自定义**：通过广泛的设置定制应用程序。

- **灵活的模型支持**：选择多个 AI 模型以满足您的特定需求。

- **扩展支持**：通过最少的 Python 编程添加自定义 LLM、TTS、STT、头像、提示和其他功能

- **配置文件支持**：使用我们的配置文件功能快速切换完全不同的设置

## 推荐的 LLM 和模型
您完全可以自由选择使用哪些模型和提供商来使用 Nyarch Assistant。
默认情况下，Nyarch Assistant 使用我们的演示 API（限制为 10 次请求/天），该 API 对其他所有内容使用 `gemini-flash-2.0`。这些 API **只是为了展示 Nyarch Assistant**，您应该**使用带有 API 密钥的另一个提供商**或使用 **Ollama** 或我们的内置加载器使用本地模型。

如果不支持您想要的提供商，您可以[制作自己的扩展](https://github.com/qwersyk/Newelle/wiki/Developing-extensions)或[查看现有扩展](https://github.com/qwersyk/Newelle/wiki/User-guide-to-Extensions#finding-extensions)。

- 对于一般用途、常识、编码和角色扮演，建议使用 `Llama3.1-70B+` 模型。
- 如果您做更多编程/IT 相关的事情，建议使用 `qwen3-8b`+、`deepseek-r1`、`deepseek-v3`、`Mixtral8x22B`、`claude-3.5-sonnet` 模型（基本上任何大小）。
- 仅用于角色扮演，您可能喜欢 `qwen3-4b`+、`mythomax-l2-13b`、`llama3.1-7B`、`gemma3` 模型或 `wizardlm-2-8x22b`。

**有关如何设置不同提供商的更多信息，请阅读** [Newelle 的 LLM 用户指南](https://github.com/qwersyk/Newelle/wiki/User-guide-to-the-available-LLMs)
## Nyarch Assistant 设置建议
### 最大隐私
使用这些设置，所有内容都将在本地运行，不会向任何地方发送有关您的数据。

由于这些计算需要大量资源，建议使用良好的 GPU 以获得良好的性能。
#### 本地 LLM
支持两个离线模型提供商：GPT4All（或"本地模型"）和 Ollama（推荐）。有关如何设置它们的说明，请阅读 [Newelle Wiki - 本地模型](https://github.com/qwersyk/Newelle/wiki/User-guide-to-the-available-LLMs#local-models-1)。
**建议使用 Ollama 的模型，因为它具有更多功能和通常更好的性能。**
有关推荐的模型，请阅读[推荐的 LLM 和模型](#推荐的-llm-和模型)
#### TTS
最好支持的具有自然声音的本地 TTS 是 `Vits` 和 `VoiceVox`。如果您有不错的 Nvidia GPU（RTX 系列），TTS 应该几乎是即时的。在其他情况下，可能需要一些加载时间。
##### VoiceVox
[VoiceVox](https://voicevox.hiroshiba.jp/) 是一个开源 TTS 引擎，日语听起来非常自然。

由于它只支持日语，如果您不懂日语，您可以决定启用翻译。
###### 安装和使用 VoiceVox
如果您启用了智能提示，您可以要求 Arch-chan 指导您完成这些步骤！如果您不相信她的话，这里是完整的说明。

**步骤 1**：安装 docker
```bash
sudo pacman -S docker
sudo systemctl enable --now docker
```

如果您有 **Nvidia GPU** 并且想要使用它，还要安装 `nvidia-container-toolkit`。此外，**必须安装 Nvidia 专有驱动程序。**
```bash
sudo pacman -S nvidia-container-toolkit
sudo systemctl restart docker.service
```
**步骤 2**：安装 docker 容器

如果您想使用 **仅 CPU**：
```bash
sudo docker pull voicevox/voicevox_engine:cpu-ubuntu20.04-latest
```

如果您想使用 **Nvidia GPU**：
```bash
sudo docker pull voicevox/voicevox_engine:nvidia-ubuntu20.04-latest
```
**步骤 3**：启动容器

如果在 **cpu** 上：
```bash
sudo docker run --rm -it -p '127.0.0.1:50021:50021' voicevox/voicevox_engine:cpu-ubuntu20.04-latest
```

如果在 **gpu** 上：
```bash
sudo docker run --rm --gpus all -p '127.0.0.1:50021:50021' voicevox/voicevox_engine:nvidia-ubuntu20.04-latest
```

**每次您想使用 voicevox 时都必须启动容器**

**步骤 4**：在 Nyarch Assistant 设置中配置它
![immagine](https://github.com/user-attachments/assets/426e73d7-b2ca-4f05-9674-fd43d06ff647)

将 `http://localhost:50021` 作为端点（或者如果您在其他地方托管它，则使用您选择的 ip/端口）。
然后，关闭并重新打开设置以重新加载语音，然后选择您最喜欢的语音。
##### 语音克隆
您可以使用[此扩展](https://github.com/FrancescoCaracciolo/Newelle-Voice-Cloning)使用 TTS 进行语音克隆。

# DeepVid Skill · 知影

让 AI Agent 使用 DeepVid 桌面客户端，将视频、音频整理为图文笔记，并检索你的本地知识库。

Give your AI agent the ability to digest videos and audio into illustrated notes and search your local knowledge library with the DeepVid desktop app.

## 能做什么

- 精读视频、音频链接与本机媒体文件。
- 根据已有图文笔记回答问题，复用知识库中的内容。
- 按需引导安装、启动客户端、配置模型与连接 DeepVid MCP。
- 处理用户选定的媒体目录，先确认范围再执行。

## 下载

当前版本：**v0.1.0**。

直接下载 [DeepVid Skill v0.1.0 ZIP](https://github.com/977star/DeepVid-Skill/releases/download/v0.1.0/deepvid-skill-v0.1.0.zip)，或前往[最新发布页](https://github.com/977star/DeepVid-Skill/releases/latest)。解压后会得到 `deepvid-skill` 文件夹，无需 Git 或下载整个项目。

更新时下载新版本，替换原技能目录中的文件，再按所用 Agent 的要求刷新或重新加载技能。技能版本独立于桌面客户端版本，版本号记录在 `VERSION` 文件中。

## 安装与使用

将本仓库作为一个名为 `deepvid-skill` 的技能目录，安装到你的 Agent 支持的技能位置。目录中应直接包含 `SKILL.md`、`agents/` 和 `references/`，具体安装方式以所用 Agent 的说明为准。

安装后可尝试：

```text
使用 $deepvid-skill 帮我精读这个视频：https://视频链接
```

Skill 是操作指南；安装它不会自动安装桌面客户端或注册 MCP 连接。首次使用时会按实际缺项引导配置。需要能够访问客户端所在电脑的 Agent；云端沙箱的 localhost 不是你的电脑。

## 运行条件与费用

- 需要 [DeepVid 桌面客户端](https://deepvid.977star.com)保持运行。
- 通过客户端设置中的 DeepVid MCP 连接知识库与任务服务。
- 新视频精读需要配置语音识别与笔记模型；在线模型可能产生所选提供商的费用。
- 本技能不授予客户端付费权益，具体能力以客户端实际返回为准。
- 不要将 MCP 密钥、模型 API Key 或浏览器 Cookie 提交到仓库。

[官网](https://deepvid.977star.com) · [客户端下载](https://github.com/977star/DeepVid/releases/latest)

---

## English

### What it does

- Digest video/audio links and local media into illustrated notes.
- Answer questions using existing notes in your knowledge library.
- Guide desktop installation, model setup, and DeepVid MCP connection when needed.
- Process a media folder after confirming the scope with you.

### Download and install

Download [DeepVid Skill v0.1.0](https://github.com/977star/DeepVid-Skill/releases/download/v0.1.0/deepvid-skill-v0.1.0.zip), or visit the [latest release](https://github.com/977star/DeepVid-Skill/releases/latest). Extract the ZIP and install the `deepvid-skill` folder in your agent's supported skills location. No Git is required.

Try: “Use $deepvid-skill to digest this video: <video URL>.”

For updates, download the new release, replace the skill files, and reload skills as required by your agent. The skill has its own version, recorded in `VERSION`, independent of the desktop app.

### Requirements and costs

The [DeepVid desktop app](https://deepvid.977star.com) must be running and connected through DeepVid MCP. Installing the skill does not install the app or register an MCP connection automatically; the skill guides you through missing setup steps.

Use an agent that can access the computer running DeepVid. A remote sandbox's localhost is not your computer. New digests require speech recognition and a note-generation model; online providers may charge for usage. Client feature availability depends on your actual permissions. Never commit MCP keys, model API keys, or browser cookies to this repository.

[Website](https://deepvid.977star.com) · [Desktop downloads](https://github.com/977star/DeepVid/releases/latest)

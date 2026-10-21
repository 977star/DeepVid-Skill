# DeepVid Skill · 知影

让 AI Agent 使用 DeepVid 桌面客户端，将视频、音频整理为图文笔记，并检索你的本地知识库。

## 能做什么

- 精读视频、音频链接与本机媒体文件。
- 根据已有图文笔记回答问题，复用知识库中的内容。
- 按需引导安装、启动客户端、配置模型与连接 DeepVid MCP。
- 处理用户选定的媒体目录，先确认范围再执行。

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

## 文件说明

| 文件 | 内容 |
| --- | --- |
| [SKILL.md](SKILL.md) | 技能入口与工作流程 |
| [agents/openai.yaml](agents/openai.yaml) | Agent 展示信息 |
| [references/desktop.md](references/desktop.md) | 客户端获取、安装与启动 |
| [references/mcp.md](references/mcp.md) | MCP 连接与恢复 |
| [references/digest.md](references/digest.md) | 模型配置、精读与结果读取 |

[官网](https://deepvid.977star.com) · [客户端下载](https://github.com/977star/DeepVid/releases/latest)

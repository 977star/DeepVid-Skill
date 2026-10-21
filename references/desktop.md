# 客户端获取、安装与启动

仅在客户端缺失、未启动或用户询问安装时读取。不依赖知影源码目录、Python 开发环境、Ego 或额外技能。此目录是独立分发的 Skill 资料，不是客户端运行资源。

## 1. 确定运行位置与平台

先用宿主提供的本机系统信息判断操作系统和 CPU 架构。没有本机权限就询问用户，不用远程 Linux 沙箱的系统信息判断用户电脑。当前目标是 macOS、Windows；其他系统只给官方信息，不提供未经验证的原生安装承诺。

先检查知影是否已连接、运行或安装，避免重复下载。macOS 检查 `/Applications/DeepVid.app`、`~/Applications/DeepVid.app`；Windows 按下方注册表/安装目录定位。若服务探测可用，检查 `http://127.0.0.1:54977/api/health` 返回是否确为知影（当前为 `{"status":"ok","app":"Omni-Video-Digest"}`）。端口有响应本身不足以确认；不要对陌生服务发送密钥。

## 2. 获取官方下载地址

- 官网：<https://deepvid.977star.com>
- 正式用户版清单：<https://download.977star.com/deepvid/version.json>
- 官方发布页：<https://github.com/977star/DeepVid/releases/latest>
- 官方 GitHub 最新 Release API：<https://api.github.com/repos/977star/DeepVid/releases/latest>

优先从用户版清单读取已发布的 `platforms`/`assets`；不可用时读取官方 Release。版本号、文件名和是否支持该架构以实际清单为准，不写死源码版本，不猜下载 URL，不从构建仓或镜像站取测试产物。

当前清单的常见结构：`platforms["darwin-aarch64"].url` / `platforms["windows-x64"].url`，带有 `fallback_url`；`assets` 项为 `name`、`browser_download_url`、`fallback_url`。结构可能变化，先读再选择。Apple Silicon 匹配 aarch64/arm64 DMG，Windows 匹配实际支持的架构；Intel Mac/Windows ARM 无匹配资产时说明尚未找到，不能擅自声称兼容。官网/发布页是 HTML，不是安装包。

下载前说明来源、匹配的平台、版本，以及可得的包大小，取得下载同意。首选用户真实的“下载”目录：macOS 通常为 `~/Downloads`；Windows 优先系统 Downloads Known Folder（可能重定向至其他盘或 OneDrive），只有确认后才使用 `%USERPROFILE%\Downloads`。不以当前工作目录或远程沙箱目录冒充用户下载目录。

通过宿主下载能力或可靠的本机下载工具将包保存为独立文件，正确处理空格、中文与同名文件，不覆盖已有文件。仅使用上述官方来源解析出的 HTTPS 资产；GitHub 资产可重定向至其官方资产分发域名。记录最终绝对路径，检查 HTTP/下载成功、实际字节数和文件类型，不把错误 HTML 或未完成的临时文件当成包；有官方校验和时比对。失败时只尝试清单给出的官方回退源一次，仍失败则给官网下载入口并停下。

## 3. 安装：与下载分开询问

包已落盘后告知完整路径，询问是否尝试安装并启动，按宿主可用权限执行。不要照搬 Ego 安装脚本中的移除隔离标记、提权覆盖或自动删除旧应用逻辑。

### macOS

常规方式是打开 DMG，让用户将 DeepVid 拖到 Applications，再由用户完成首次打开确认。允许自动文件操作且用户明确同意时，可挂载 DMG、验证镜像中的 `DeepVid.app` 后安装到已确认的位置，再正常卸载镜像；目标位置已有应用就优先使用现有安装，不静默覆盖。

若系统阻止首次打开，交给用户完成正常的系统确认。不要移除 Gatekeeper/隔离属性、关闭系统保护或索取管理员密码。挂载与复制是否成功都要验证，不因启动了复制命令就宣称已安装。

### Windows

打开已下载的官方 NSIS `.exe` 安装器，通常使用交互安装；现有包是当前用户安装模式。引导用户完成路径选择和系统确认。不要把“可以安装”解释为同意 UAC 提权或静默覆盖旧安装；无人值守方式仅在用户明确授权且目标安装器参数经过确认时使用。

**不能自动安装时**：给出安装包完整路径和简短步骤，经用户同意可打开安装包所在目录。macOS 可用 `open -R "实际安装包绝对路径"`；Windows 可用 `explorer.exe /select,"实际安装包绝对路径"`。这些是模板，按实际宿主传参并正确引用路径。等待用户确认完成，不在后台连续下载/重试安装。

## 4. 启动已安装应用

仅在用户同意启动，或已有适用于本次视频请求的持续启动授权时执行。优先原生启动方式，不直接运行内部 Sidecar，也不终止其他进程。

macOS 在确认路径存在后：

```sh
open "/Applications/DeepVid.app"
```

如安装在用户 Applications 或用户指定位置，使用检测到的真实路径。

Windows 按顺序读取已存在的安装信息并验证 `DeepVid.exe` 文件：

1. HKCU `Software\DeepVid\DeepVid` 默认值。
2. HKCU `Software\977Star✨\DeepVid` 默认值（历史/当前安装器兼容键）。
3. HKCU `Software\Microsoft\Windows\CurrentVersion\Uninstall\DeepVid` 的 `InstallLocation`（如实际存在）。
4. `%LOCALAPPDATA%\Programs\DeepVid\DeepVid.exe` 等已确认的默认路径；找不到时请用户指定安装位置或从开始菜单打开，不扫描整块硬盘。

通过原生应用启动接口或 `explorer.exe "实际安装目录\DeepVid.exe"` 启动；支持工作目录的接口将其设为该 EXE 所在目录。不要假定 `DeepVid.exe` 已加入 PATH。

## 5. 等待就绪与失败交接

本机权限允许时，以短超时健康请求检查服务；启动后每隔约 2 秒检查一次，最多约 60 秒，等待期间保持简短进度反馈。确认知影健康响应后再进入 MCP 验证；健康成功不代表 MCP 已启用、密钥有效或模型就绪。

超时就停下，给出尝试的应用路径，请用户确认客户端能否正常打开；不无限重启。若用户需要手动操作，说明“打开后告诉我，我会继续连接刚才的视频”，不自动越过下一步。

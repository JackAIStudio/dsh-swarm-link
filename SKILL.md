---
name: dsh-swarm-link
description: >
  多机协同与节点互联互通框架。允许当前 DSH Agent 发现、控制并与同一网络/外网下的其他 PC、Mac 或云服务器进行交互和文件传输。
  当用户要求“让台式机帮我做…”、“把这个文件传给云端”、“检查另外一台机器的状态”时调用本技能。
---

# dsh-swarm-link: 通用节点互联与控制指南

你当前身处一个“多设备 AI 集群”中。你可以通过 SSH 协议指派其他机器完成任务或传输文件。

## 1. 节点发现与寻址
当用户要求你跨设备执行任务时，你必须先执行以下命令读取集群配置文件：
`cat ~/.dsh/peers.yaml`
仔细阅读其中的 `peers` 列表，找到与用户描述相匹配的节点 `id`、`os`、`ssh_user`、`ssh_host` 和 `ssh_port`。

## 2. 跨设备执行任务 (命令下发)
确定目标节点后，你可以直接通过本地 `bash` 工具利用 SSH 向对端下发指令。
- **通用语法**：`ssh -p <ssh_port> <ssh_user>@<ssh_host> '<你要对端执行的 bash 命令>'`
- **注意**：如果对端的 `os` 是 Windows，请发送兼容 CMD/PowerShell 的命令；如果是 macOS/Linux，请发送标准 shell 命令。
- **示例**：如果用户让你“看一台式机的 CPU 占用率”，你可以使用 `ssh -p 22 Administrator@192.168.1.101 'wmic cpu get loadpercentage'`。

## 3. 跨设备文件传输 (文件调度)
你可以使用 `scp` 在当前机器和集群节点之间移动文件。
- **发送文件到对端**：`scp -P <ssh_port> <本地文件路径> <ssh_user>@<ssh_host>:<目标路径>`
- **从对端拉取文件**：`scp -P <ssh_port> <ssh_user>@<ssh_host>:<目标文件路径> <本地保存路径>`

## 4. 故障诊断
如果 SSH 命令返回 `Connection refused` 或超时，说明对端掉线。请明确告知用户该节点（如“win-desktop”）目前不可达，并建议用户检查设备的开机或网络状态。

## 执行铁律
1. **绝对不要**在未经用户允许的情况下，尝试猜测或暴力破解未在 `peers.yaml` 中列出的 IP。
2. 跨设备执行复杂或破坏性命令（如 `rm -rf`，大文件移动）前，请向用户简述你即将通过 SSH 发送的底层命令，并请求确认。

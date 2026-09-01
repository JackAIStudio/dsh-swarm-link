# DSH Swarm Link 🌐

一个轻量、通用的多设备 AI 节点互联框架，将多台设备上的 DeepSeek Harness（Mac、Windows、Linux 云服务器）串联成私有分布式工作台。

---

## 🤖 方式一：让 Agent 自动帮我安装（推荐 ⭐️）

如果你正在使用 DeepSeek Harness 或其他 AI Agent 编程工具，**无需手动敲命令**，直接将以下提示词复制并发送给你的 Agent：

> **“请帮我安装 `JackAIStudio/dsh-swarm-link` 技能：**
> 1. 将 `SKILL.md` 保存到我的技能目录 `~/.agents/skills/dsh-swarm-link/SKILL.md`；
> 2. 如果我的 `~/.dsh/peers.yaml` 不存在，参考 `peers.yaml.example` 帮我初始化一个模板，并引导我填入我的设备 IP。”

---

## 👨‍💻 方式二：人类手动安装指南

如果你喜欢手动掌控每一步：

### 1. 安装 Skill 规则文件
```bash
mkdir -p ~/.agents/skills/dsh-swarm-link
cp SKILL.md ~/.agents/skills/dsh-swarm-link/
```

### 2. 初始化节点配置文件
```bash
cp peers.yaml.example ~/.dsh/peers.yaml
```
用编辑器打开 `~/.dsh/peers.yaml`，填入你的局域网电脑或云服务器的 IP、端口和用户名。

### 3. 打通 SSH 免密 (核心前提)
在当前机器终端运行一次，确保免密直连对端：
```bash
ssh-copy-id -p <端口> <用户名>@<目标IP>
```

---

## 🌟 核心能力
- **跨设备任务分发**：在轻薄本上指挥性能台式机跑模型或重度任务；
- **跨端文件秒传**：一句话让云端处理好的文件、图片隔空回传到本地桌面；
- **节点灾难自愈**：利用大模型的推理能力，在对端服务掉线时代为执行拉起与修复。

## 💬 使用示例 (直接对 Agent 说大白话)
- *“帮我把刚才生成的图片传到我另一台电脑的桌面上”*
- *“检查一下书房的台式机还在不在线”*
- *“让云端服务器帮我跑一下这个抓取任务”*

---

## 📄 License
MIT License. 欢迎 Star ⭐️ 与贡献 PR！

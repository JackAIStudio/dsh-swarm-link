# dsh-swarm-link 仓库与 Agent 维护规范（AGENTS.md）

> 本文件是本项目的**代码架构与维护硬性规范**。
> 所有 AI Agent 与人类贡献者在修改、重构或新增功能时，**必须严格遵守以下规则**。

---

## 1. 零单文件膨胀原则（Strict File Size Limits）

1. **单文件行数上限**：
   - 任何单个源码文件严禁超过 **300 行**。
   - 保持小而美，严禁将多节点探测、文件流式转发、集群同步逻辑无脑塞进单文件。
2. **模块职责划分建议**：
   - `lib/discovery.js`：节点发现与探活。
   - `lib/sync.js`：跨端数据传输与安全校验。
   - `lib/cluster.js`：集群配置读取与状态维护。

---

## 2. 安全与跨平台铁律

1. **凭据安全**：
   - 严禁将 `peers.yaml`、集群私钥或敏感 Token 提交进 Git 仓库。
2. **跨平台路径**：
   - 统一使用 `node:path` 与 `os.homedir()`，严禁硬编码 macOS 的绝对路径。

---

## 3. 修改后自检

修改任何代码后，必须运行以下命令进行语法验证：
```bash
find . -name "*.js" -o -name "*.mjs" -not -path "*/.*" -not -path "*/node_modules/*" -exec node --check {} +
```

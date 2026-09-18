# 元忆 yotta-memory — Agent Plugin

File-based agent memory with permission boundaries, packaged as an Agent Plugin with a built-in MCP server (remember / recall / search / context).

[English](#english) | [中文](#中文)

## English

This repository is a standalone [Agent Plugins 1.0](https://agent-plugins.org) plugin. It packages one skill and one MCP server in the standard layout (`plugin.json`, `skills/`, `mcp.json`).

### Install

#### Codex (verified)

```bash
codex plugin marketplace add YottaMeta/yotta-memory-plugin
codex plugin add yotta-memory@yotta-memory
```

#### Other compatible clients

Agent Plugins defines the package format, not a universal installer command. Use your client’s official setup instructions:

| Client | Setup instructions |
| --- | --- |
| VS Code | [Agent Plugins in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-plugins) |
| Cursor | [Cursor plugins](https://cursor.com/docs/plugins) |
| GitHub Copilot | [About plugins](https://docs.github.com/en/copilot/concepts/agents/about-plugins) |
| ChatGPT & Codex | [OpenAI plugins](https://developers.openai.com/plugins) |
| Kiro | [Powers](https://kiro.dev/docs/powers/) |
| Hermes Agent | [Portable Agent Plugins v1 packages](https://hermes-agent.nousresearch.com/docs/developer-guide/plugins#portable-agent-plugins-v1-packages) |
| OpenClaw | [Plugin bundles](https://docs.openclaw.ai/plugins/bundles) |
| Grok Bot | [Skills, routines, and automations](https://docs.x.ai/grok-bot/skills-routines-and-automations) |
| NanoClaw | [Templates](https://github.com/nanocoai/nanoclaw/blob/main/docs/templates.md) |

Codex is verified by YottaMeta. Other clients are linked from the official Agent Plugins compatibility page and are not yet verified here.

### What you get

- **Skill** — `yotta-memory` skill instructions (`skills/yotta-memory/SKILL.md`)
- **MCP server** — started automatically by the client (stdio; requires Node.js)

### Identity handshake (host substitution)

This plugin ships `mcp.json` with identity placeholders (`${AGENT_ID}, ${AGENT_KEY_FILE}`). The client/installer must replace them when assembling the MCP server; the raw placeholder values are not usable.

- `${AGENT_ID}` — this agent's unique id (single path segment; no `/`, `\`, `..`).
- `${AGENT_KEY_FILE}` — path to the `agent_key` file for that id, created by the user via `yotta-memory view` and `yotta-memory key claim <id>`; the default is `<AI_HOME>/.yotta-memory-agent-key`.

Without a replaced identity the server still starts, but private memory operations (PREF / BOUND / COMMIT) fail closed; public FACT operations keep working. The v0.16.0 stdio identity contract accepts only `--agent-id` + `--agent-key-file`; identity environment variables are no longer read.


### Boundaries

- The MCP server runs fully local over stdio; no telemetry, no remote calls from the plugin itself.
- If the required runtime is missing, the MCP component may fail to start; the skill payload remains available.
- The skill payload is copied from the source repository release; for full documentation see [YottaMeta/yotta-memory](https://github.com/YottaMeta/yotta-memory).

### Source

Upstream skill repository: [YottaMeta/yotta-memory](https://github.com/YottaMeta/yotta-memory)
Plugin repository: [YottaMeta/yotta-memory-plugin](https://github.com/YottaMeta/yotta-memory-plugin)

### License

MIT — see `LICENSE` and the license inside the skill payload.

## 中文

本仓库是一个独立的 [Agent Plugins 1.0](https://agent-plugins.org) 插件，按标准目录结构打包一项技能和一个 MCP server（`plugin.json`、`skills/`、`mcp.json`）。

### 安装

#### Codex（已实测）

```bash
codex plugin marketplace add YottaMeta/yotta-memory-plugin
codex plugin add yotta-memory@yotta-memory
```

#### 其他兼容客户端

Agent Plugins 只定义包格式，不定义统一安装命令。请按你所用客户端的官方说明接入：

| 客户端 | 官方说明 |
| --- | --- |
| VS Code | [Agent Plugins in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-plugins) |
| Cursor | [Cursor plugins](https://cursor.com/docs/plugins) |
| GitHub Copilot | [About plugins](https://docs.github.com/en/copilot/concepts/agents/about-plugins) |
| ChatGPT & Codex | [OpenAI plugins](https://developers.openai.com/plugins) |
| Kiro | [Powers](https://kiro.dev/docs/powers/) |
| Hermes Agent | [Portable Agent Plugins v1 packages](https://hermes-agent.nousresearch.com/docs/developer-guide/plugins#portable-agent-plugins-v1-packages) |
| OpenClaw | [Plugin bundles](https://docs.openclaw.ai/plugins/bundles) |
| Grok Bot | [Skills, routines, and automations](https://docs.x.ai/grok-bot/skills-routines-and-automations) |
| NanoClaw | [Templates](https://github.com/nanocoai/nanoclaw/blob/main/docs/templates.md) |

Codex 已由 YottaMeta 实测；其他客户端仅链接官方说明，尚未在本仓库逐项实测。

### 内容

- **技能** — `yotta-memory` 技能指令（`skills/yotta-memory/SKILL.md`）
- **MCP server** — 由客户端自动启动（stdio；需要 Node.js）

### 身份装配（宿主替换占位符）

本插件发布的 `mcp.json` 带身份占位符（`${AGENT_ID}, ${AGENT_KEY_FILE}`），客户端 / 安装器在装配 MCP server 时必须替换，未替换的原始值不可用。

- `${AGENT_ID}` — 本智能体的唯一 id（单段名称，禁止 `/`、`\`、`..`）。
- `${AGENT_KEY_FILE}` — 该 id 的 `agent_key` 文件路径，由用户执行 `yotta-memory view` 授权后经 `yotta-memory key claim <id>` 领取，默认 `<AI_HOME>/.yotta-memory-agent-key`。

宿主未替换身份时 server 仍可启动，但私密记忆（PREF / BOUND / COMMIT）操作 fail-closed，公共 FACT 不受影响。v0.16.0 的 stdio 身份契约只接受 `--agent-id` + `--agent-key-file`，不再读取身份环境变量。


### 边界

- MCP server 完全本地 stdio 运行；插件本身不做遥测、不发起远程调用。
- 若运行时缺失，MCP 组件可能启动失败；技能内容仍可使用。
- 技能内容来自源仓库发布版；完整文档见 [YottaMeta/yotta-memory](https://github.com/YottaMeta/yotta-memory)。

### 来源

上游技能仓库：[YottaMeta/yotta-memory](https://github.com/YottaMeta/yotta-memory)
插件仓库：[YottaMeta/yotta-memory-plugin](https://github.com/YottaMeta/yotta-memory-plugin)

### 许可证

MIT — 见 `LICENSE` 与技能目录内许可证。

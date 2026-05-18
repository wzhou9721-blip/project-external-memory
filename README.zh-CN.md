# Project External Memory

一个用于 Codex 的 skill，用来在长对话、上下文压缩、重启和未来会话之间保留项目交接状态。

这个 skill 的核心思路是：通过 `AGENTS.md` 把项目绑定到一个简洁的项目记忆文件。这个记忆文件不是聊天记录，也不是只追加不整理的流水账，而是一份“当前可用的交接文档”：过期状态要替换，已经失效的快照要删除，只有在时间线真的有价值时才把历史细节归档。

## 它能做什么

- 为项目添加或更新 `AGENTS.md` 中的连续性规则。
- 创建一个主要的项目记忆文件。
- 让项目状态保持简洁、当前、可操作。
- 提醒 Codex 在做判断前先读取项目记忆。
- 提醒 Codex 在完成重要变更后更新项目记忆。

## 适合什么时候用

适合长期项目、运维项目、服务、机器人、监控、迁移任务，或者任何你希望未来 Codex 会话不用依赖聊天历史也能理解当前状态的项目。

示例请求：

```text
Use project-external-memory to set up durable memory for this repo.
```

```text
Update the project memory after this deployment change.
```

```text
Review the external memory and compact stale notes.
```

## 安装

把 `project-external-memory` 文件夹复制到你的 Codex skills 目录：

```text
~/.codex/skills/project-external-memory
```

Windows 上通常是：

```text
C:\Users\<YOU>\.codex\skills\project-external-memory
```

## 仓库结构

```text
project-external-memory/
  SKILL.md
  agents/
    openai.yaml
  references/
    templates.md
```

## 使用建议

skill 本体保持通用，不应该写入某个具体项目的名称、路径或业务状态。

每个项目自己的触发词、路径、当前状态、运维说明和风险记录，应该放在该项目的 `AGENTS.md` 和主记忆文件里。

## 设计原则

- 记忆文件是当前交接文档，不是聊天存档。
- 优先替换旧状态，而不是不断追加新段落。
- 不保存密钥、token、私人聊天或大段日志。
- 只保存未来会话真正需要知道的 durable state。
- 主记忆文件应该短到每次开工前都能快速读完。

# Agent Team Builder Skill

通过 7 步结构化问答引导用户从零设计多 Agent 协作团队，最终输出可直接部署的 `agents_team_spec.md`。

**跨平台支持：Kun · ChatGPT · Claude Code · DeepSeek · Cursor · Hermes · Gemini · 更多**

## 快速开始

选择你的平台：

| 平台 | 操作 |
|---|---|
| **Kun** | 直接使用 — Skill 自动激活 |
| **ChatGPT** | 创建 Custom GPT，粘贴 `adapters/system-prompt.md` |
| **Claude Code** | 复制 `adapters/CLAUDE.md` 到项目根目录 |
| **DeepSeek / Hermes / 其他** | 将 `adapters/system-prompt.md` 粘贴到 System Prompt |

详细步骤见 [`adapters/README.md`](adapters/README.md)。

然后对 AI 说：

> 帮我设计一个 Agent 团队

Agent 将按 7 步流程逐一询问，最终生成完整的团队规格说明书。

## 文件结构

```
.
├── .agents/skills/agent-team-builder/
│   └── SKILL.md              # Skill 定义（Kun 原生格式，含 YAML frontmatter + triggers）
├── adapters/
│   ├── README.md             # 跨平台适配指南
│   ├── system-prompt.md      # 通用 System Prompt（ChatGPT / DeepSeek / Hermes / Gemini...）
│   └── CLAUDE.md             # Claude Code 适配版
├── agent_team_builder.md      # 人类阅读版 Skill 设计文档
└── README.md                  # 本文件
```

## Skill 覆盖范围

- 项目目标确认
- 任务模块拆解（3~10 个）
- Sub Agent 角色/技能/输入/输出定义
- 通信协议与工作流拓扑设计
- 责任矩阵与修复闭环
- 身份注册与工作空间管理
- Manager Agent 启动 Prompt 模板
- 完整 JSON 通讯录模板示例

## 适用场景

软件开发、内容创作、数据分析、产品设计、市场运营等任何需要多 Agent 协作的复杂任务。

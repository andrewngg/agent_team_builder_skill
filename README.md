# Agent Team Builder Skill

通过 7 步结构化问答引导用户从零设计多 Agent 协作团队，最终输出可直接部署的 `agents_team_spec.md`。

## 快速开始

将 `.agents/skills/agent-team-builder/SKILL.md` 加载到任意支持 Skill 的 AI Agent 中，然后对 Agent 说：

> 帮我设计一个 Agent 团队

Agent 将按 7 步流程逐一询问，最终生成完整的团队规格说明书。

## 文件结构

```
.
├── .agents/skills/agent-team-builder/
│   └── SKILL.md          # Skill 定义（AI Agent 可执行指令）
└── agent_team_builder.md  # 人类阅读版 Skill 设计文档
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

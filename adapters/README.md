# 跨平台适配指南

Agent Team Builder Skill 的核心内容（7 步交互流程 + 模板）是**平台无关**的——任何 AI Agent 读到都能执行。区别只在于不同平台如何注入这段指令。

## 快速对照表

| 平台 | 适配文件 | 操作方式 |
|---|---|---|
| **Kun** | `.agents/skills/agent-team-builder/SKILL.md` | 自动识别 YAML frontmatter + triggers，无需手动操作 |
| **ChatGPT (Custom GPT)** | `adapters/system-prompt.md` | 创建 Custom GPT → 粘贴全文到 Instructions 字段 |
| **DeepSeek GUI** | `adapters/system-prompt.md` | 开新对话 → 粘贴全文作为第一条消息（附言："请按此流程执行"） |
| **Hermes / OpenRouter** | `adapters/system-prompt.md` | 粘贴到 System Prompt 字段 |
| **Claude Code** | `adapters/CLAUDE.md` | 重命名为 `CLAUDE.md` 放到项目根目录；或用 `/init` 导入 |
| **Cursor** | `adapters/system-prompt.md` | 粘贴到 `.cursorrules` 或 Cursor Settings → Rules for AI |
| **Gemini / Qwen / 其他** | `adapters/system-prompt.md` | 粘贴到 System Prompt 或 Custom Instructions 字段 |

## 各平台详细用法

### 1. ChatGPT (Custom GPT)

1. 打开 [ChatGPT Custom GPT 创建页](https://chatgpt.com/gpts/editor)
2. Name: `Agent Team Builder`
3. Description: `通过 7 步结构化问答帮你从零设计多 Agent 协作团队`
4. Instructions: 粘贴 `adapters/system-prompt.md` 全文
5. Conversation starters 可选：
   - `帮我设计一个 Agent 团队`
   - `我想搭建一个多 Agent 协作系统`
6. 保存 → 每次对话时选择这个 Custom GPT 即可

### 2. DeepSeek GUI / DeepSeek API

DeepSeek GUI 没有独立的 System Prompt 输入框，但两种方式都可行：

**方式 A（GUI 第一条消息）：**
```
请将以下内容作为你的系统指令，严格按照其中的 7 步流程执行：

[粘贴 adapters/system-prompt.md 全文]

收到请回复"已就绪，请描述你的项目"。然后等待我输入。
```

**方式 B（API）：**
将 `system-prompt.md` 全文放入 API 的 `system` 消息字段。

### 3. Claude Code

```bash
# 方式 A：作为项目级 CLAUDE.md
cp adapters/CLAUDE.md ./CLAUDE.md

# 方式 B：用 /init 导入
# 在 Claude Code 对话中输入 /init，然后粘贴 CLAUDE.md 全文
```

Claude Code 会在每次对话启动时自动加载 `CLAUDE.md`。

### 4. Cursor

1. 打开 Cursor Settings → General → Rules for AI
2. 粘贴 `adapters/system-prompt.md` 全文
3. 或在项目根目录创建/编辑 `.cursorrules` 文件

### 5. Hermes / OpenRouter / 通用 API

将 `adapters/system-prompt.md` 全文放入 API 请求的 `system` 消息字段：

```json
{
  "model": "hermes-3",
  "messages": [
    {
      "role": "system",
      "content": "[adapters/system-prompt.md 全文]"
    },
    {
      "role": "user",
      "content": "帮我设计一个 Agent 团队"
    }
  ]
}
```

### 6. Kun（原生支持）

无需任何适配。将整个 repo 克隆到 Kun 的 workspace 下，Skill 的 `triggers` 会自动匹配用户输入。

---

## 适配原理

| 组件 | Kun SKILL.md | 通用适配版 | 说明 |
|---|---|---|---|
| YAML frontmatter | ✅ 需要 | ❌ 删除 | Kun 用 `triggers` 做自动激活，其他平台不需要 |
| `name` / `description` | ✅ 需要 | ❌ 删除 | 仅 Kun 的 Skill 注册系统使用 |
| 7 步流程正文 | ✅ | ✅ 完全相同 | 核心指令，所有平台共用 |
| 附录模板 | ✅ | ✅ 完全相同 | 示例和 JSON 模板，所有平台共用 |

**一句话总结：去掉 YAML 头，剩下的就是通用版。**

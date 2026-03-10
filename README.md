<p align="center">
  <img src="logo.svg" alt="Context Handoff Logo" width="128" height="128">
</p>

<h1 align="center">Context Handoff Skill</h1>

<p align="center">
  <strong>Preserve conversation context across Claude Code sessions</strong>
</p>

<p align="center">
  <a href="#english">English</a> | <a href="#中文介绍">中文</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License">
  <img src="https://img.shields.io/badge/claude--code-skill-blue.svg" alt="Claude Code Skill">
</p>

---

## English

### What is this?

A Claude Code skill that helps you preserve conversation context when switching to a new chat session. It generates structured handoff documents that capture decisions, progress, blockers, and user preferences — so the next session can pick up exactly where you left off.

### Why do you need this?

Claude Code conversations have context limits. When you hit the limit mid-task, you lose:
- Key decisions and their reasoning
- Rejected approaches (and why they were rejected)
- User preferences discovered during the conversation
- Progress on multi-step tasks

This skill solves that by creating a "save point" you can load in a new conversation.

### Features

| Command | Description |
|---------|-------------|
| `/handoff` | Generate a handoff document from current conversation |
| `/handoff load <keyword>` | Load a previous handoff document to restore context |
| `/handoff list` | List recent handoff documents |

### What gets captured?

- **Task status**: In progress / Completed / Blocked
- **Completed steps**: What's been done, with key outputs
- **Todo items**: Prioritized (🔴 high / 🟡 medium / 🟢 low)
- **Blockers**: What's stuck and why
- **Key decisions**: The choice made, alternatives considered, and reasoning
- **Rejected approaches**: What didn't work and why (prevents re-treading)
- **User preferences**: Communication style, workflow preferences, terminology

### Installation

1. Copy the `context-handoff` folder to your Claude Code skills directory:
   ```bash
   cp -r context-handoff ~/.claude/skills/
   ```

2. Update the save path in `SKILL.md` to match your system:
   ```markdown
   **保存路径**：`/your/path/to/handoff/documents/`
   ```

### Usage

**Generate a handoff:**
```
/handoff
```
Claude will extract key information, ask you to confirm, then save the document.

**Restore context in a new session:**
```
请读取 /path/to/handoff/document.md 恢复上下文，然后告诉我摘要和待办。
```
Or use:
```
/handoff load <keyword>
```

### Document Structure

Handoff documents use a structured format with:
- YAML frontmatter for metadata
- `<ai_context>` tags for AI-priority parsing (reduces token usage on restore)
- Obsidian-compatible markdown (works as regular markdown too)

### License

MIT

---

## 中文介绍

### 这是什么？

一个 Claude Code 技能，帮助你在切换到新对话时保留上下文。它生成结构化的交接文档，记录决策、进度、阻塞项和用户偏好——让下一个会话能从中断处无缝继续。

### 为什么需要它？

Claude Code 对话有上下文限制。当你在任务中途触及限制时，你会丢失：
- 关键决策及其推理过程
- 被否决的方案（以及为什么被否决）
- 对话中发现的用户偏好
- 多步骤任务的进度

这个技能通过创建「存档点」来解决这个问题，你可以在新对话中加载它。

### 功能

| 命令 | 说明 |
|------|------|
| `/handoff` | 从当前对话生成交接文档 |
| `/handoff load <关键词>` | 加载之前的交接文档恢复上下文 |
| `/handoff list` | 列出最近的交接文档 |

### 会记录什么？

- **任务状态**：进行中 / 已完成 / 遇阻
- **已完成步骤**：做了什么，关键产出
- **待办事项**：按优先级标记（🔴 高 / 🟡 中 / 🟢 低）
- **阻塞项**：卡在哪里，为什么
- **关键决策**：选择了什么方案、考虑过的替代方案、选择理由
- **被否决的方案**：什么没用、为什么（避免重复踩坑）
- **用户偏好**：沟通风格、工作流偏好、约定术语

### 安装

1. 将 `context-handoff` 文件夹复制到 Claude Code 技能目录：
   ```bash
   cp -r context-handoff ~/.claude/skills/
   ```

2. 修改 `SKILL.md` 中的保存路径为你的系统路径：
   ```markdown
   **保存路径**：`/你的/交接文档/保存路径/`
   ```

### 使用方法

**生成交接文档：**
```
/handoff
```
Claude 会提取关键信息，让你确认后保存文档。

**在新会话中恢复上下文：**
```
请读取 /path/to/handoff/document.md 恢复上下文，然后告诉我摘要和待办。
```
或使用：
```
/handoff load <关键词>
```

### 文档结构

交接文档使用结构化格式：
- YAML frontmatter 存储元数据
- `<ai_context>` 标签标记 AI 优先解析的内容（恢复时减少 token 消耗）
- Obsidian 兼容的 Markdown（也可作为普通 Markdown 使用）

### 设计原则

**细节保留原则**：压缩目的是「快速恢复沟通状态」，不是「缩短文档长度」。宁长不丢。

### 许可证

MIT

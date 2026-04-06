# Project-Level AGENTS Rules Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create a project-level `AGENTS.md` that constrains this repository to brainstorming and Chinese document output only.

**Architecture:** Add one root `AGENTS.md` as the repository-wide rule file and keep the existing design spec as the authoritative rationale. The implementation is documentation-only: define scope, repository purpose, mandatory workflow, redirect rules, and output standards without introducing any code path.

**Tech Stack:** Markdown, Git, shell verification (`rg`, `sed`, `git diff --check`)

---

## Planned Files

- Create: `AGENTS.md`

### Task 1: Create The Project-Level Rule File

**Files:**
- Create: `AGENTS.md`

- [ ] **Step 1: Write the root rule document**

```md
# AGENTS.md

## Scope

本文件是本仓库的项目级规则文档，适用于整个仓库。

在本仓库内，Codex 必须优先遵循本文件定义的工作方式。

## Repository Purpose

本仓库只用于以下用途：

- 使用 `brainstorm` 做脑暴
- 梳理调研要求
- 设计问题清单
- 澄清需求边界
- 沉淀中文文档

本仓库不是代码实现仓库。

在这个仓库内，不以交付功能、修复代码、生成补丁或完成开发实现为目标。

## Output Audience

本仓库产出的正式文档默认写给以下对象使用：

- `GPT-5.4 Pro` 等具备深度检索能力的模型
- 后续负责执行调研的人类研究员

因此，所有正式文档都必须写成可直接交给下游执行者使用的材料，而不是随意的聊天记录、零散笔记或泛泛建议。

## Mandatory Workflow

在本仓库内处理任何正式任务时，Codex 必须遵循以下流程：

1. 先进入 `brainstorm`
2. 在写正式文档前，至少完成 `10` 个脑暴问题
3. 所有问题都必须使用选择题形式
4. 每次提问都必须给出至少 `3` 个选项
5. 在用户完成选择后，再整理正式文档
6. 所有正式文档统一写入 `docs/superpowers/plans/`

不得跳过问题阶段直接开始写正式文档。

“至少 10 个问题”是硬性流程要求，不是建议项。

## Interaction Rules

本仓库内的用户交互默认使用选择题。

Codex 提问时：

- 不应把关键澄清问题写成开放式大问答
- 必须提供至少 `3` 个可选项
- 可以允许用户在选项基础上微调，但整体交互形式仍然应以选择题为主

## Allowed Output

本仓库只允许产出中文文档。

允许的正式产出包括：

- 调研任务书
- 提问模板
- 需求澄清文档
- 约束整理文档
- 执行要求文档
- 结构化脑暴结论

不应把正式产出写到 `docs/superpowers/plans/` 之外的其他目录。

## Redirect Rules

如果用户在本仓库内要求以下事项：

- 写代码
- 改功能
- 修 bug
- 生成补丁
- 直接交付实现

Codex 必须先明确提醒用户：这个仓库不能这么用。

然后，Codex 必须把请求重定向为：

- 先进行 `brainstorm`
- 先完成至少 `10` 个选择题问题
- 最终只产出中文文档

在这个仓库内，不存在跳过脑暴直接进入实现的路径。

## Output Standard

本仓库内的正式文档必须满足以下标准：

- 使用中文
- 结构清晰
- 约束明确
- 边界明确
- 可直接交给下游强模型或研究员执行
- 尽量减少歧义
- 不写成随意建议或松散笔记

## Priority

如果用户的请求与本仓库用途不一致，优先保持本仓库的文档定位，并先提醒用户当前请求不适合在这个仓库中直接执行。
```

- [ ] **Step 2: Verify the file contains all required sections**

Run: `rg '^## ' AGENTS.md`
Expected:

```text
## Scope
## Repository Purpose
## Output Audience
## Mandatory Workflow
## Interaction Rules
## Allowed Output
## Redirect Rules
## Output Standard
## Priority
```

- [ ] **Step 3: Verify the rule file enforces the 10-question and 3-option constraints**

Run: `rg -n '10|3|选择题|brainstorm|docs/superpowers/plans/' AGENTS.md`
Expected: output includes the mandatory workflow and interaction rules lines

- [ ] **Step 4: Commit the rule file**

```bash
git add AGENTS.md
git commit -m "docs: add project-level AGENTS rules"
```

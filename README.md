# interactive-skill

用一个可复用 skill 解决 Agent 交互常见痛点：
- 问题问得多但价值低
- 改代码前没有对齐，返工高
- 进度汇报不结构化，审批成本高

## What is included

- `AGENTS.md`
  - Codex 项目协议（运行时真源）
  - 定义提问上限、checkpoint 粒度、命令白名单

- `CLAUDE.md`
  - Claude Code 侧的同等工作协议
  - 与 `AGENTS.md` 保持一致的交互规则

- `spec-align` skill（核心）
  - 只问高价值问题（最多 3 个）
  - 每个问题包含：Why it matters / Evidence / Default assumption
  - 先输出 Assumption Ledger、验收标准与阶段 checkpoint，再进入实现

## Repository structure

```text
.
├── AGENTS.md
├── CLAUDE.md
├── README.md
├── .agents
│   └── skills
│       └── spec-align
│           └── SKILL.md
└── .claude
    └── skills
        └── spec-align
            └── SKILL.md
```

## Installation

### 1) 准备一个目标仓库

```bash
cd /path/to/your-project
```

### 2) 拷贝协议和 skill 文件

把 `<interactive-skill-path>` 替换成这个仓库所在路径。

```bash
mkdir -p .agents/skills/spec-align .claude/skills/spec-align

cp <interactive-skill-path>/AGENTS.md ./AGENTS.md
cp <interactive-skill-path>/CLAUDE.md ./CLAUDE.md
cp <interactive-skill-path>/.agents/skills/spec-align/SKILL.md ./.agents/skills/spec-align/SKILL.md
cp <interactive-skill-path>/.claude/skills/spec-align/SKILL.md ./.claude/skills/spec-align/SKILL.md
```

### 3) 校验安装是否完成

```bash
test -f AGENTS.md && test -f CLAUDE.md && echo "protocol files ready"
find .agents/skills/spec-align .claude/skills/spec-align -type f | sort
```

## Push to GitHub

` .agents `、` .claude ` 这种点目录可以正常提交到 GitHub。  
常见问题是使用了 `git add *`，它不会包含点目录。

请用：

```bash
git add -A
git commit -m "chore: add agent interaction protocol and skills"
git push
```

如果只想加这几个文件，也可以显式写路径：

```bash
git add README.md AGENTS.md CLAUDE.md .agents .claude
git commit -m "chore: add agent interaction protocol and skills"
git push
```

## Quick start

1. 在 Codex 或 Claude Code 中，先运行 `spec-align` 完成需求对齐。
2. 对齐通过后再开始改动，并按 phase checkpoint 汇报进度。
3. 调整交互风格时，只改这三行：
   - `MAX_CLARIFY_QUESTIONS_PER_ROUND`
   - `CHECKPOINT_GRANULARITY`
   - `COMMAND_ALLOWLIST`

## Defaults

- `MAX_CLARIFY_QUESTIONS_PER_ROUND = 3`
- `CHECKPOINT_GRANULARITY = phase`
- `COMMAND_ALLOWLIST = test,lint,format`

## Why this setup

这个最小结构优先解决“先对齐再动手”的问题，避免 Agent 在需求不清时直接修改仓库造成返工。后续如需执行型流程，可再补 `ship-plan`。

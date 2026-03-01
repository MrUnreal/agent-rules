# agent-rules

Universal coding agent rules that work across **GitHub Copilot**, **Claude Code**, and **Cursor**.

## Why?

Every coding agent community has its own "top 10 tips" — but the best practices are agent-agnostic. This repo distills general skills (not technology-specific recipes) into a single canonical rules file that all major agents can consume.

## How it works

```
AGENTS.md                          ← canonical rules (read by ALL agents)
├── CLAUDE.md                      ← imports AGENTS.md via @-syntax
├── .github/copilot-instructions.md← Copilot custom instructions
└── .cursor/rules/general-skills.mdc ← Cursor project rules
```

| Agent | How it finds the rules |
|-------|------------------------|
| **GitHub Copilot** | Reads `AGENTS.md` + `.github/copilot-instructions.md` from repo root |
| **Claude Code** | Reads `CLAUDE.md` (which imports `AGENTS.md`) + `.claude/` skills |
| **Cursor** | Reads `AGENTS.md` + `.cursor/rules/*.mdc` |

### One source of truth

`AGENTS.md` is the single canonical file. Agent-specific files either import it or contain a lightweight reference. When you improve a rule, you improve it once.

## Usage

### Option 1: Clone into your project
```bash
git clone https://github.com/MrUnreal/agent-rules.git .agent-rules
# then copy or symlink the files you need into your project root
```

### Option 2: Copy individual files
Grab `AGENTS.md` and drop it into any repo. Every major agent reads it natively.

### Option 3: Git submodule
```bash
git submodule add https://github.com/MrUnreal/agent-rules.git .agent-rules
```

## Rules overview

The rules are organized into these categories:

1. **Meta-Rule** — how to research, iterate, and write rules (the rule that governs all other rules)
2. **Exploration & Planning** — understand before you act
3. **Verification & Testing** — always prove your work
4. **Context Management** — be precise, stay focused
5. **Iterative Development** — small steps, tight loops
6. **Communication** — ask, explain, report
7. **Code Quality** — conventions, clarity, consistency
8. **Anti-Patterns** — what NOT to do

## Contributing

This repo follows its own meta-rule:

1. **Research** — find authoritative sources and real-world patterns
2. **Iterate** — distill into clear, agent-agnostic directives
3. **Write** — add to `AGENTS.md` (the canonical file)
4. **Research more** — validate, refine, repeat

PRs welcome. Focus on general skills, not technology-specific recipes.

## Sources

- [Claude Code Best Practices](https://code.claude.com/docs/en/best-practices)
- [Addy Osmani — The Prompt Engineering Playbook](https://addyo.substack.com/p/the-prompt-engineering-playbook-for)
- [Harper Reed — My LLM Codegen Workflow](https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/)
- [agents.md Standard](https://github.com/anthropics/agents.md)
- [GitHub Copilot Custom Instructions](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)
- [Cursor Rules Documentation](https://docs.cursor.com/context/rules)
- [Claude Code Settings Documentation](https://code.claude.com/docs/en/settings)

## License

MIT

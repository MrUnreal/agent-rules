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
| **OpenAI Codex** | Reads `AGENTS.md` natively from repo root |

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

## Rules (23 total)

| # | Rule | One-Liner |
|---|------|-----------|
| 0 | Meta-Rule | Research → synthesize → write → validate → repeat |
| 1 | Explore First | Read the codebase before changing it |
| 2 | Plan First | Break tasks into steps before implementing |
| 3 | Verify Work | Test, lint, and confirm after every change |
| 4 | Small Steps | One logical change at a time |
| 5 | Manage Context | Stay focused, be specific, seed with existing code |
| 6 | Communicate | Ask when unclear, explain when acting |
| 7 | Quality Code | Follow conventions, handle errors, be explicit |
| 8 | Structured Workflows | Follow the right workflow for the task type |
| 9 | Delegate | Parallelize independent work, use subagents |
| 10 | Avoid Anti-Patterns | No kitchen sinks, no over-correction, no skipping failures |
| 11 | Red/Green TDD | Write tests first, confirm they fail, then implement |
| 12 | Knowledge Assets | Hoard working examples; agents can recombine them |
| 13 | Cognitive Debt | Understand your code; don't let it become a black box |
| 14 | Agent Environments | Design tests, logs, and progress files for agent consumption |
| 15 | Iterate, Don't One-Shot | Expect multi-turn refinement; bad first results are starting points |
| 16 | Precise Specifications | Dictate signatures, provide examples, constrain the solution space |
| 17 | Know When to Take Over | Recognize when the agent is stuck; read docs yourself; split the work |
| 18 | Guard Long-Term Quality | Watch for verbose tests, lack of reuse, and brute-force fixes |
| 19 | Build Context Incrementally | Start minimal; add rules from real failures, not theory |
| 20 | Treat Failures as Signals | Fix the system (docs, linters, tests), not just the prompt |
| 21 | Security-Conscious Use | Vet MCP servers, apply least privilege, guard against approval fatigue |
| 22 | Calibrate Review Depth | Assess probability × impact × detectability to decide review effort |

## Contributing

This repo follows its own meta-rule:

1. **Research** — find authoritative sources and real-world patterns
2. **Iterate** — distill into clear, agent-agnostic directives
3. **Write** — add to `AGENTS.md` (the canonical file)
4. **Research more** — validate, refine, repeat

PRs welcome. Focus on general skills, not technology-specific recipes.

## Sources

- [Claude Code Best Practices](https://code.claude.com/docs/en/best-practices)
- [Simon Willison — Agentic Engineering Patterns](https://simonwillison.net/guides/agentic-engineering-patterns/)
- [Simon Willison — Here's how I use LLMs to help me write code](https://simonwillison.net/2025/Mar/11/using-llms-for-code/)
- [Addy Osmani — Agentic Engineering](https://addyosmani.com/blog/agentic-engineering/)
- [Addy Osmani — The Prompt Engineering Playbook](https://addyo.substack.com/p/the-prompt-engineering-playbook-for)
- [Nicholas Carlini — Building a C Compiler with Parallel Claudes](https://www.anthropic.com/engineering/building-c-compiler)
- [Harper Reed — My LLM Codegen Workflow](https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/)
- [OpenAI — Introducing Codex](https://openai.com/index/introducing-codex/)
- [Anthropic — Building Effective Agents](https://www.anthropic.com/research/building-effective-agents)
- [Birgitta Böckeler / Martin Fowler — Context Engineering for Coding Agents](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html)
- [Birgitta Böckeler / Martin Fowler — The Role of Developer Skills in Agentic Coding](https://martinfowler.com/articles/exploring-gen-ai/13-role-of-developer-skills.html)
- [Birgitta Böckeler / Martin Fowler — Harness Engineering](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html)
- [Birgitta Böckeler — To Vibe or Not to Vibe](https://martinfowler.com/articles/exploring-gen-ai/to-vibe-or-not-vibe.html)
- [Birgitta Böckeler — I Still Care About the Code](https://martinfowler.com/articles/exploring-gen-ai/i-still-care-about-the-code.html)
- [Matteo Vaccari — Partner with the AI, Throw Away the Code](https://martinfowler.com/articles/exploring-gen-ai/partner-with-ai-and-throw-away-the-code.html)
- [Aider — Tips and Conventions](https://aider.chat/docs/usage/tips.html)
- [Mitchell Hashimoto — My AI Adoption Journey](https://mitchellh.com/writing/my-ai-adoption-journey)
- [Gumbley & Ryan — Coding Assistants Threaten the Software Supply Chain](https://martinfowler.com/articles/exploring-gen-ai/software-supply-chain-attack-surface.html)
- [agents.md Standard](https://github.com/anthropics/agents.md)
- [GitHub Copilot Custom Instructions](https://docs.github.com/en/copilot/customizing-copilot/adding-repository-custom-instructions-for-github-copilot)
- [Cursor Rules Documentation](https://docs.cursor.com/context/rules)
- [Claude Code Settings Documentation](https://code.claude.com/docs/en/settings)

## License

MIT

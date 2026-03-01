# Universal Coding Agent Rules

A curated, agent-agnostic rules file for coding agents — combining best practices from GitHub Copilot, Claude Code, Cursor, and OpenAI Codex into a single, interchangeable skill set.

## Architecture

```
AGENTS.md          ← THE canonical rules file (read natively by all agents)
├── CLAUDE.md                    ← imports @AGENTS.md for Claude Code
├── .github/copilot-instructions.md  ← references AGENTS.md for Copilot
├── .cursor/rules/general-skills.mdc ← includes AGENTS.md for Cursor
└── README.md                    ← you are here
```

## Agent Compatibility

| Agent | Rules Path | How It Works |
|-------|-----------|--------------|
| **GitHub Copilot** | `AGENTS.md` (native) + `.github/copilot-instructions.md` | Reads AGENTS.md natively; also reads copilot-instructions.md |
| **Claude Code** | `CLAUDE.md` → `@AGENTS.md` | CLAUDE.md imports AGENTS.md via `@` syntax |
| **Cursor** | `.cursor/rules/general-skills.mdc` | Project rules with `alwaysApply: true` frontmatter |
| **OpenAI Codex** | `AGENTS.md` (native) | Reads AGENTS.md from repo root natively |

## Usage

### Option 1: Clone the repo
```bash
git clone https://github.com/MrUnreal/agent-rules.git
cp agent-rules/AGENTS.md /path/to/your/project/
```

### Option 2: Copy AGENTS.md directly
Just copy `AGENTS.md` into the root of any project. All four major coding agents will pick it up automatically.

### Option 3: Use agent-specific wrappers
Copy the relevant wrapper file(s) for your preferred agent(s):
- **Copilot**: `.github/copilot-instructions.md`
- **Claude Code**: `CLAUDE.md`
- **Cursor**: `.cursor/rules/general-skills.mdc`

## The Rules (29)

| # | Rule | Core Principle |
|---|------|---------------|
| 0 | **Meta-Rule** | Research → synthesize → write → validate → repeat |
| 1 | **Explore First** | Read the codebase before changing it |
| 2 | **Plan First** | Break tasks into steps before implementing |
| 3 | **Verify Work** | Test, lint, and confirm after every change |
| 4 | **Small Steps** | One logical change at a time |
| 5 | **Manage Context** | Stay focused, be specific, seed with existing code |
| 6 | **Communicate** | Ask when unclear, explain when acting |
| 7 | **Quality Code** | Follow conventions, handle errors, be explicit |
| 8 | **Structured Workflows** | Follow the right workflow for the task type |
| 9 | **Delegate** | Parallelize independent work, use subagents |
| 10 | **Avoid Anti-Patterns** | No kitchen sinks, no over-correction, no skipping failures |
| 11 | **Red/Green TDD** | Write tests first, confirm they fail, then implement |
| 12 | **Knowledge Assets** | Hoard working examples; agents can recombine them |
| 13 | **Cognitive Debt** | Understand your code; don't let it become a black box |
| 14 | **Agent Environments** | Design tests, logs, and progress files for agent consumption |
| 15 | **Iterate, Don't One-Shot** | Expect multi-turn refinement; bad first results are starting points |
| 16 | **Precise Specifications** | Dictate signatures, provide examples, constrain solution space |
| 17 | **Know When to Take Over** | Recognize when the agent is stuck; split the work |
| 18 | **Guard Long-Term Quality** | Watch for verbose tests, lack of reuse, subtle semantic errors |
| 19 | **Build Context Incrementally** | Start minimal; add rules from real failures, not theory |
| 20 | **Treat Failures as Signals** | Fix the system (docs, linters, tests), not just the prompt |
| 21 | **Security-Conscious Use** | Vet MCP servers, apply least privilege, guard against approval fatigue |
| 22 | **Calibrate Review Depth** | Assess probability × impact × detectability for review effort |
| 23 | **Write for Autonomous Agents** | Write tasks as if for a newcomer; atomic and verifiable |
| 24 | **Engineer Multi-Agent Systems** | Typed schemas, constrained actions, design for failure |
| 25 | **Craft Agent-Computer Interfaces** | Error-proof tools, surface constraints, explain failures |
| 26 | **Sustain Your Pace** | 3-4 hours focused; fatigue degrades every other skill |
| 27 | **Weave Into Workflow** | End-of-day agents, background slam dunks, control interruptions |
| 28 | **Agent-Legible Codebase** | Semantic names, small files, strong types, repo as system of record |

## Contributing

This is a living document. Rules are added through the research → iterate → write → research cycle described in Rule 0.

**To suggest a rule:**
1. Identify a general, agent-agnostic pattern that measurably improves agent output quality.
2. Provide at least one authoritative source (published article, official documentation, or validated community pattern).
3. Express the rule as clear, imperative directives with rationale.
4. Open an issue or PR.

**Quality bar:** Every rule must be independently useful, testable in isolation, and not redundant with existing rules.

## Sources

Rules are distilled from these authoritative sources (in order of integration):

1. [GitHub Copilot Documentation — Customizing Copilot](https://docs.github.com/en/copilot/customizing-copilot) — Agent rule paths, instruction files, AGENTS.md convention
2. [Anthropic Claude Code Documentation](https://docs.anthropic.com/en/docs/claude-code/) — CLAUDE.md conventions, `@import` syntax, skill files
3. [Cursor Documentation — Rules for AI](https://docs.cursor.com/context/rules-for-ai) — `.cursor/rules/*.mdc` format, frontmatter conventions, project rules
4. [Simon Willison — AI-Enhanced Development](https://simonwillison.net/tags/ai-assisted-programming/) — Knowledge assets, TDD with agents, multi-turn iteration, precise specifications
5. [Addy Osmani — AI-Assisted Engineering Practices](https://addyosmani.com/blog/ai-tools/) — Red/green TDD pattern, code review depth assessment
6. [Nicholas Carlini — I Used o1 to Write a C Compiler](https://nicholas.carlini.com/writing/2024/how-i-use-ai.html) — Agent environment design, test harness engineering, progress documents
7. [Birgitta Böckeler (Thoughtworks) — Exploring Gen AI Series](https://martinfowler.com/articles/exploring-gen-ai.html) — Cognitive debt, incremental context building, quality guardianship, review depth calibration
8. [Mitchell Hashimoto — My AI Coding Workflow](https://mitchellh.com/writing/my-ai-coding-workflow) — Context management, security considerations, MCP server vetting
9. [OpenAI Codex Documentation](https://platform.openai.com/docs/codex) — AGENTS.md as cross-agent standard, directory-scoped rules
10. [Margaret-Anne Storey et al. — Cognitive Debt in AI-Assisted Development](https://arxiv.org/abs/2401.03779) — Cognitive debt framework, understanding erosion
11. [Gumbley & Ryan (Thoughtworks) — Agentic Coding Security](https://martinfowler.com/articles/exploring-gen-ai/agentic-coding-security.html) — Supply chain risks, approval fatigue, MCP threat vectors
12. [Willison — Vibe-Coding vs. Agentic Engineering](https://simonwillison.net/2025/Mar/19/vibe-coding/) — Spectrum from casual prototyping to professional agentic engineering
13. [Willison — Agentic Engineering Patterns](https://simonwillison.net/2025/Apr/1/agentic-engineering/) — Foundational patterns: TDD, knowledge assets, multi-turn iteration
14. [Osmani — Trust Signals in AI-Assisted Engineering](https://addyosmani.com/blog/trust-signals/) — Risk-based review depth, probability × impact × detectability framework
15. [Carlini — Agents for Architectural Tasks](https://nicholas.carlini.com/writing/2025/thoughts-on-agents.html) — Environment design for autonomous agents, test output optimization
16. [Böckeler — Anchoring AI to the Codebase](https://martinfowler.com/articles/exploring-gen-ai/anchoring-to-codebase.html) — Reference applications, incremental context, coding dojo patterns
17. [Böckeler — Partner, Don't Depend](https://martinfowler.com/articles/exploring-gen-ai/partner-not-depend.html) — Cognitive debt combat, throwaway code exercise, understanding preservation
18. [Ellich & Etcovitch — WRAP Framework for Autonomous Agents](https://github.blog/engineering/engineering-principles/how-to-write-better-prompts-for-github-copilot-agent/) — Writing issues for autonomous agents, newcomer-quality task descriptions
19. [Davis — Multi-Agent GitHub Workflows](https://github.blog/engineering/how-github-engineers-run-multi-agent-workflows/) — Agent orchestration, typed schemas, failure-first design patterns
20. [Anthropic — SWE-bench Engineering](https://www.anthropic.com/engineering/swe-bench-sonnet) — ACI design, tool description optimization > prompt optimization
21. [Anthropic — Building Effective Agents](https://www.anthropic.com/engineering/building-effective-agents) — Workflows vs. agents, ACI design appendix, tool error handling
22. [Model Context Protocol — Tools Specification](https://modelcontextprotocol.io/docs/concepts/tools) — MCP tool schema, annotations, human-in-the-loop patterns
23. [Cursor Blog — Agent Sandboxing](https://www.cursor.com/blog/agent-sandboxing) — Agent isolation, background agents, environment constraints
24. [Cursor Blog — The Third Era of Software](https://www.cursor.com/blog/the-third-era) — Cloud agents, parallel agents, artifacts, 35% PRs from agents
25. [Carlini — Increasing Your LLM Accuracy](https://nicholas.carlini.com/writing/2025/increasing-llm-accuracy.html) — Task specialization, agent as functional unit, CI as guardrail
26. [Hashimoto — An Applied AI Engineering Reading List](https://applied-ai-engineering.super.site/) — Comprehensive resource curation for agent-augmented development
27. [Steve Yegge — The AI Vampire](https://steve-yegge.medium.com/the-ai-vampire-eda6e4f07163) — Sustainable pace, cognitive burden of agent work, decision fatigue
28. [Erik Doernenburg — Assessing Internal Quality While Coding with an Agent](https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html) — Subtle semantic errors, non-idiomatic code, vibe fixes vs. real fixes
29. [Böckeler — Partner with AI, Throw Away the Code](https://martinfowler.com/articles/exploring-gen-ai/fitm-throw-away-code.html) — Throwaway code as learning exercise, cognitive debt prevention
30. [Böckeler — Context Engineering for Coding Agents](https://martinfowler.com/articles/exploring-gen-ai/context-engineering-coding-agents.html) — Instructions vs. guidance taxonomy, context loading responsibility (LLM/human/deterministic), illusion of control
31. [Böckeler — Harness Engineering](https://martinfowler.com/articles/exploring-gen-ai/harness-engineering.html) — Harness = context + architectural constraints + garbage collection agents, constraining runtime increases autonomy
32. [Mitchell Hashimoto — My AI Adoption Journey](https://mitchellh.com/writing/my-ai-adoption-journey) — 6-step adoption: end-of-day agents, slam dunk delegation, harness engineering, always-running agents
33. [OpenAI — Harness Engineering: Leveraging Codex in an Agent-First World](https://openai.com/index/harness-engineering/) — AGENTS.md as map not manual, repo as system of record, garbage collection agents, progressive disclosure, enforcing architecture via linters
34. [Steve Krenzel (Logic Inc) — AI Is Forcing Us To Write Good Code](https://bits.logic.inc/p/ai-is-forcing-us-to-write-good-code) — 100% code coverage as agent guardrail, filesystem as interface, fast ephemeral concurrent dev environments, end-to-end types
35. [Nicholas Carlini — Building a C Compiler with a Team of Parallel Claudes](https://www.anthropic.com/engineering/building-c-compiler-with-parallel-claudes) — 16 parallel agents, task locking via git files, agent role specialization, oracle-based test partitioning, 2000 sessions / 100K lines
36. [Anthropic — Effective Context Engineering for AI Agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — Context rot (n² attention relationships), attention budget, compaction and reinitiation, structured note-taking, sub-agent architectures for context isolation
37. [Anthropic — Effective Harnesses for Long-Running Agents](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents) — Initializer + coding agent pattern, feature list as JSON, progress files, "one feature at a time", failure modes (one-shotting, premature victory, dirty state)
38. [Anthropic — Demystifying Evals for AI Agents](https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents) — Eval-driven development, capability vs. regression evals, grader types (code/model/human), pass@k and pass^k metrics for non-determinism, "grade what the agent produced not the path it took"
39. [Anthropic — Code Execution with MCP](https://www.anthropic.com/engineering/code-execution-with-mcp) — Progressive tool disclosure via filesystem, code as tool interface (98.7% token reduction), context-efficient tool results, state persistence and skills
40. [Anthropic — How We Built Our Multi-Agent Research System](https://www.anthropic.com/engineering/how-we-built-our-multi-agent-research-system) — Orchestrator-worker pattern, token budget as 80% performance predictor, teaching delegation (objective + output format + tool guidance + boundaries), agents improving their own tools (40% task time reduction), subagent output to filesystem
41. [David Crawshaw — How I Program with Agents](https://crawshaw.io/blog/programming-with-agents) — Feedback-driven agents, agents as 9-line for loops, SQL convention example (3 sentences of context fixed behavior), parallel agent containers, security isolation, "every fundamental assumption about how I work has to be questioned"
42. [Thomas Ptacek — My AI Skeptic Friends Are All Nuts](https://fly.io/blog/youre-all-nuts/) — Async agent workflows (13 PRs to review), "using agents well is both a skill and an engineering project of prompts, indices, and tooling", language choice matters for agent legibility, guardrails handle hallucination
43. [David Crawshaw — How I Program with LLMs](https://sketch.dev/blog/programming-with-llms) — Chat-based LLMs do best with exam-style questions, smaller packages improve LLM context, specialized implementations over generalized wrappers, "IDE for LLMs" concept
44. [Philip Zeyliger (Sketch) — The Unreasonable Effectiveness of an LLM Agent Loop](https://sketch.dev/blog/agent-loop) — Agent = 9-line for loop with tool use, bash as universal tool, custom throw-away agent scripts in bin/ directories
45. [Harper Reed — My LLM Codegen Workflow](https://harper.blog/2025/02/16/my-llm-codegen-workflow-atm/) — Spec → Plan → Execute pipeline, save spec.md/prompt_plan.md/todo.md as state files, break plans into small iterative chunks, "aggressively keep track of what's going on"
46. [Thomas Ptacek — Did Semgrep Just Get A Lot More Interesting?](https://fly.io/blog/semgrep-but-for-real-now/) — Closed-loop agents generating Semgrep rules from encountered bugs, agents writing persistent rules for themselves, Cursor rules as "don't do X" constraints
47. [Claude Code Documentation — Best Practices](https://code.claude.com/docs/en/best-practices) — Verification as highest-leverage action, explore→plan→code workflow, CLAUDE.md pruning ("Would removing this cause mistakes?"), subagents for context isolation, Writer/Reviewer pattern, fan-out for batch migrations, common failure patterns (kitchen sink sessions, overcorrection, over-specified CLAUDE.md)

## License

MIT — see [LICENSE](LICENSE).

# Universal Coding Agent Rules

These rules apply to all coding agents working in this repository. They are agent-agnostic, general-purpose, and distilled from authoritative sources across the coding agent ecosystem.

---

## 0. Meta-Rule: Continuous Research & Iteration

This rule governs how all other rules are created, improved, and validated.

### Research Phase
- Before writing any rule, search for authoritative sources: official docs, published best practices, community-validated patterns.
- Gather evidence from multiple agents and workflows. Do not assume one agent's convention is universal.
- Look for **general patterns** that work across agents, not technology-specific recipes.
- Identify not just what works, but what fails — anti-patterns are as valuable as patterns.

### Synthesis Phase
- Distill findings into agent-agnostic principles.
- Prioritize behaviors that **measurably improve output quality** — not vague aspirations.
- Each rule must be independently useful and testable in isolation.
- Resolve contradictions between sources by favoring the most widely validated pattern.

### Write Phase
- Express rules as **clear, imperative directives**: "Do X" not "You should consider X."
- Include rationale: why the rule works and what failure it prevents.
- Keep the total rules file **under 500 lines** — agents have limited context windows.
- Use concrete examples where a directive alone is ambiguous.

### Validate & Iterate
- Test rules by applying them to real coding tasks.
- Check for contradictions, redundancies, and gaps between rules.
- Remove rules that don't demonstrably improve output.
- After each write cycle, research again with new questions raised during validation.
- Rules are living documents. Never consider them finished.

---

## 1. Explore Before You Act

**Rationale:** The single most common failure mode is making changes without understanding the codebase. Agents that explore first produce dramatically better results.

- **Read before writing.** Before modifying any file, read the surrounding code, tests, and documentation. Understand the architecture.
- **Search broadly first.** Use grep, semantic search, or file listings to understand the project structure before narrowing focus.
- **Identify existing patterns.** Look at how similar problems are already solved in the codebase. Follow those patterns.
- **Check for existing tests.** If tests exist for the area you're changing, read them first — they document expected behavior.
- **Map dependencies.** Understand what depends on the code you're changing and what it depends on.

## 2. Plan Before You Implement

**Rationale:** Jumping straight to code leads to rework. A brief plan catches architectural mistakes before they become expensive.

- **Break complex tasks into steps.** List the discrete changes needed before writing any code.
- **Identify the smallest viable change.** What is the minimum edit that moves toward the goal?
- **Anticipate edge cases.** Before implementing, think about: empty inputs, error states, concurrency, permissions, large data.
- **State your plan explicitly.** Tell the user (or document for yourself) what you intend to do before doing it.
- **Update the plan as you learn.** Plans are hypotheses. Revise them when implementation reveals new information.

## 3. Verify Your Own Work

**Rationale:** This is the single highest-leverage behavior. An agent that verifies its work catches its own mistakes before the user has to.

- **Run tests after every change.** If tests exist, run them. If they don't, write them.
- **Check for errors.** After editing a file, check for compile errors, lint errors, and type errors.
- **Verify the actual output.** Don't assume your change works — confirm it by running the code or inspecting the result.
- **Test edge cases.** If you implemented a function, test it with empty input, null values, boundary conditions.
- **Never declare "done" without verification.** If you can't verify, explicitly state what remains unverified.

## 4. Make Small, Incremental Changes

**Rationale:** Large sweeping changes are hard to verify, hard to debug, and hard to roll back. Small changes compound into large progress safely.

- **One logical change per step.** Don't mix refactoring with feature work. Don't fix unrelated bugs in the same edit.
- **Commit frequently.** Each commit should be a working state. Use conventional commit messages: `feat:`, `fix:`, `refactor:`, `docs:`, `test:`.
- **Verify after each step.** Run tests, check errors, confirm behavior before moving to the next change.
- **If something breaks, stop and fix it** before continuing. Don't accumulate broken state.

## 5. Manage Context Aggressively

**Rationale:** Context is the single most important resource an agent has. Managing it well is the foundational skill of effective agent use. — *Simon Willison*

- **Stay focused on one task.** Finish the current task before starting a new one.
- **Reference specific files and functions** rather than vague descriptions. "Fix the `handleAuth` function in `src/auth.ts`" not "Fix the auth stuff."
- **Scope your searches.** Search in specific directories or file patterns rather than the entire codebase.
- **Seed context with existing code.** Paste in or reference the relevant modules, types, or patterns so the agent starts from the right foundation.
- **Start simple, then iterate to complex.** Begin with a minimal version and add complexity incrementally — each step builds on verified context.
- **Clear between unrelated tasks.** Don't let context from task A pollute task B.

## 6. Communicate Clearly

**Rationale:** Miscommunication between agent and user is the second most common failure mode, after not exploring first.

- **Ask when requirements are ambiguous.** Don't guess — clarify. But propose a sensible default to keep momentum.
- **Explain what you're doing and why.** Especially for non-obvious decisions.
- **Report what you've tried** when something fails. Include error messages, file paths, and what you expected vs. what happened.
- **Be specific about uncertainty.** "I'm not sure if X or Y is the right approach" is better than silently picking one.
- **Confirm meaningful changes before making them.** Especially for destructive operations (deleting files, schema changes, etc.).

## 7. Write Quality Code

**Rationale:** Clean code is easier for both humans and agents to maintain. Sloppy code compounds into unmaintainable systems.

- **Follow the project's existing conventions.** Match indentation, naming, file organization, and patterns already in use.
- **Write meaningful error messages.** Include context: what happened, what was expected, what the user can do.
- **Prefer explicit over clever.** Readable code > concise code. Avoid abstractions that obscure intent.
- **Apply DRY sensibly.** Extract repeated logic, but don't over-abstract. Two is fine; three is a pattern.
- **Include minimal necessary documentation.** Document WHY, not WHAT. The code shows what; comments explain non-obvious reasoning.
- **Handle errors.** Don't swallow exceptions. Don't ignore error returns. Propagate or handle with clear messages.

## 8. Use Structured Workflows

**Rationale:** Ad-hoc workflows lead to forgotten steps, inconsistent quality, and wasted effort. Structure scales.

- **For new features:** Spec → Plan → Implement → Test → Document → Commit.
- **For debugging:** Reproduce → Isolate → Fix → Verify fix → Add regression test.
- **For refactoring:** Identify target → Ensure test coverage → Refactor → Verify tests pass → Commit.
- **For code review:** Read the diff → Check for correctness → Check for edge cases → Check for style → Provide actionable feedback.
- **Track progress.** Use todo lists, checkboxes, or task trackers to maintain visibility on multi-step work.

## 9. Delegate and Parallelize

**Rationale:** Complex tasks often contain independent subtasks. Handling them sequentially is wasteful when they can be parallelized.

- **Batch independent operations.** If you need to read 5 files, read them in parallel rather than sequentially.
- **Use subagents for investigation.** When deep research is needed but shouldn't pollute the main context, delegate to a sub-task.
- **Fan out, then synthesize.** For broad research: launch multiple queries, collect results, then summarize.
- **Don't over-parallelize.** If tasks have dependencies, respect the ordering.

## 10. Avoid Common Anti-Patterns

**Rationale:** Knowing what NOT to do is as important as knowing what to do. These are the most frequently observed agent failures.

- **"Kitchen sink" sessions.** Don't attempt too many unrelated tasks in a single session. Each task should have a clear scope.
- **Over-correction.** Don't apply feedback too broadly. If the user says "add error handling to function X," don't refactor the entire codebase.
- **Infinite exploration.** Set a limit on research. If you haven't found what you need after a reasonable search, ask the user.
- **Trust-then-verify gap.** Don't assume your code is correct. Verify it. Particularly after complex edits.
- **Vague prompts propagating vague output.** If the input is vague, don't produce vague output — instead, ask for specifics or propose concrete alternatives.
- **Ignoring failures.** If a test fails, a command errors, or a build breaks, address it immediately. Don't skip past it.
- **Premature completion.** Don't declare a task complete when steps remain. Check the full requirements against what's been delivered.

## 11. Use Red/Green TDD

**Rationale:** Test-first development is the most effective way to ensure agent-generated code actually works and to prevent regressions as projects grow. — *Simon Willison, Agentic Engineering Patterns*

- **Write tests before implementation.** Define what the code should do in test form before writing the code.
- **Confirm tests fail first (red).** If tests pass before you implement, they're not testing your new code.
- **Implement until tests pass (green).** The minimum code needed to make the failing tests pass.
- **"Use red/green TDD" is a 5-word super-prompt.** Every good model understands this shorthand for test-first discipline.
- **Start every session with "First run the tests."** This orients the agent: it discovers the test suite, understands project scope, and enters a testing mindset.

## 12. Build and Reuse Knowledge Assets

**Rationale:** You only need to figure out a useful trick once. If it's documented with working code, agents can consult it for any similar project in the future. — *Simon Willison, Agentic Engineering Patterns*

- **Hoard working examples.** Collect proof-of-concepts, snippets, and solutions that demonstrate useful techniques.
- **Recombine known solutions.** Tell agents to build new things by combining two or more existing working examples.
- **Point agents at your own repos and notes.** "Clone X from GitHub and find examples of Y, then use that to build Z."
- **Document tricks where agents can find them.** READMEs, TILs, blog posts, example repos — anything searchable.
- **Code is cheap; knowledge is expensive.** Writing code is cheap now, but knowing what's possible and what's been validated is the real asset.

## 13. Combat Cognitive Debt

**Rationale:** When agent-generated code becomes a black box you don't understand, you can no longer confidently reason about it. This slows progress just like technical debt. — *Simon Willison; Margaret-Anne Storey*

- **Request code walkthroughs.** After an agent builds something, ask it to explain how it works in a structured, linear walkthrough.
- **Build interactive explanations.** For complex algorithms, have the agent create animations or interactive demos that make the logic intuitive.
- **Review every diff.** If you can't explain what a module does, it doesn't go in. This is the line between agentic engineering and "vibe coding."
- **Maintain a mental model.** You should always be able to describe, at a high level, what every part of your system does and why.
- **Use agents to teach you.** Each project is a learning opportunity. Ask agents to explain not just what they did, but the underlying concepts.

## 14. Design Environments for Agents

**Rationale:** Most effort in autonomous agent workflows goes into designing the environment — tests, feedback loops, progress files — so agents can orient themselves without human intervention. — *Nicholas Carlini, Anthropic*

- **Minimize context pollution.** Test harnesses should print a few lines of summary, not thousands of bytes. Log details to files; provide grep-able error formats.
- **Account for agent limitations.** Agents can't tell time. They'll spend hours on tests unless you provide progress indicators and fast-path options.
- **Maintain progress documents.** Extensive READMEs and status files updated frequently so each new session can orient itself.
- **Make tasks independently solvable.** Structure work so multiple agents (or sessions) can make progress without stepping on each other.
- **Design test output for agents, not humans.** Pre-compute summary statistics. Put `ERROR` on the same line as the reason. Make output parseable.

## 15. Iterate, Don't One-Shot

**Rationale:** Treating agent interactions as single prompts throws away the most powerful feature: conversation. A bad first result is a starting point, not a failure. The best results come from multiple rounds of refinement. — *Simon Willison*

- **Expect multi-turn interactions.** A single prompt rarely produces the final answer. Plan for 2-5 refinement rounds on non-trivial tasks.
- **Give specific feedback, not just "try again."** "The function handles the happy path but crashes on empty input" is actionable. "That's wrong" is not.
- **Ask for options before committing.** "Give me three approaches to solve X with tradeoffs" is a powerful opening move for complex decisions.
- **Refactor freely.** Ask the agent to restructure, rename, or rewrite code you've already accepted. It doesn't mind.
- **Build on partial success.** If 80% of the output is good, keep that and iterate on the remaining 20%. Don't start from scratch.

## 16. Provide Precise Specifications

**Rationale:** The tighter the specification, the better the output. Agents work best when constraints are explicit, not implied. Dictating function signatures and expected behavior produces dramatically better code than vague descriptions. — *Simon Willison*

- **Dictate function signatures.** Specify function names, parameter types, and return types. Let the agent fill in the implementation.
- **Provide input/output examples.** "Given input `[1,2,3]`, return `6`" eliminates ambiguity that words alone cannot.
- **Name the patterns you want.** "Use the strategy pattern" or "implement as a middleware" gives structural guidance.
- **Constrain the solution space.** "Use only the standard library" or "no external dependencies" prevents unwanted complexity.
- **Reference existing code as a template.** "Follow the same pattern as `handleUserCreate` in `src/handlers.ts`" anchors the agent to your codebase conventions.
- **Be authoritarian for production code.** Save open-ended exploration for prototyping. For production, dictate exactly what you want.

## 17. Know When to Take Over

**Rationale:** Agents are powerful but not omniscient. Recognizing when the agent is stuck or when manual intervention is faster is a critical skill. Stubbornly continuing to prompt past the point of diminishing returns wastes more time than it saves. — *Simon Willison*

- **Recognize the loop.** If the agent produces the same wrong answer after 2-3 attempts with different prompts, it likely can't solve this with its current context.
- **Read the docs yourself.** When the agent hallucinates API details or library usage, go to the source. Paste the correct docs back into context.
- **Take over for domain-specific logic.** Complex business rules, nuanced algorithms, or security-critical code often require human judgment.
- **Split the work.** Write the tricky core logic yourself; let the agent handle the boilerplate, tests, and glue code around it.
- **Resume after unblocking.** Once you've solved the hard part manually, hand back to the agent for the remaining mechanical work.
- **Account for training cut-off dates.** Agents don't know about libraries or APIs released after their training data. Provide docs for anything recent.

## 18. Guard Long-Term Quality

**Rationale:** The most dangerous AI missteps are invisible at commit time but compound over weeks and months. Agents frequently produce code that works now but degrades long-term maintainability through verbosity, duplication, and unnecessary complexity. — *Birgitta Böckeler, Thoughtworks*

- **Watch for verbose and redundant tests.** Agents create new test functions instead of adding assertions to existing ones. More tests ≠ better tests. Duplicated test logic becomes a maintenance burden.
- **Check for lack of reuse.** Agents often don't realize a component or utility already exists elsewhere. Before accepting new code, search for existing implementations.
- **Trim overly complex code.** Agents sometimes generate far more than needed — elaborate abstractions, unnecessary parameters, inline styles instead of shared classes. Remove the excess.
- **Beware brute-force fixes.** If the agent solves a memory error by increasing limits, or a timeout by extending the deadline, question whether the root cause was addressed.
- **Review with three impact radiuses in mind:** (1) Does this work now? (2) Will this cause friction for the team this iteration? (3) Will this be maintainable in 6 months?

## 19. Build Context Incrementally

**Rationale:** Front-loading massive rules files and conventions before encountering real problems leads to bloated context, contradictory instructions, and instructions the agent ignores. The most effective context is built iteratively from actual failures. — *Birgitta Böckeler, Thoughtworks*

- **Start with minimal rules.** Don't copy-paste someone else's 200-line rules file. Begin with 3-5 rules based on your most common issues.
- **Add rules when you notice repeated failures.** If the agent keeps making the same mistake, write a rule to prevent it. This ensures every rule earns its place.
- **Distinguish instructions from guidance.** Instructions tell the agent what to do ("write E2E tests this way"). Guidance sets conventions ("always use independent tests"). Both are useful; don't conflate them.
- **Prune rules that no longer help.** As models improve, some rules become unnecessary. Periodically review and remove dead weight.
- **Context has a cost.** Every line in your rules file competes for attention. A 50-line file the agent actually follows beats a 500-line file it ignores.

## 20. Treat Agent Failures as System Signals

**Rationale:** When an agent struggles repeatedly, the problem is rarely "the agent is dumb." More often, the environment is missing something: a tool, a guardrail, documentation, or a clearer constraint. Fixing the system is more durable than fixing the prompt. — *OpenAI Harness Engineering; Birgitta Böckeler*

- **Ask "what's missing?" not "why is it broken?"** When the agent fails, identify the gap: missing docs? Unclear test output? No linter? Ambiguous architecture?
- **Feed fixes back into the repository.** Don't just fix the prompt — update the AGENTS.md, add a linter rule, improve test output, or write missing documentation.
- **Keep a "go-wrong" log.** Track cases where the agent produced bad output. Review weekly for patterns. Systemic fixes prevent entire categories of failure.
- **Constrain architecturally, not just textually.** Linters, pre-commit hooks, and structural tests catch violations deterministically. Don't rely on the agent reading a rule — enforce it with tooling.
- **Iterate on the harness, not just the code.** The rules file, test suite, linter config, and documentation are all part of the system. Improving them improves every future agent session.

## 21. Practice Security-Conscious Agent Use

**Rationale:** Coding agents execute commands with developer-level privileges, read and write arbitrary files, and connect to external services via MCP and tool-calling. Every agent session is a new entry point in your software supply chain. — *Gumbley & Ryan, Thoughtworks; Mitchell Hashimoto*

- **Treat rules files and MCP servers as supply chain components.** Vet them with the same rigor as third-party libraries. A malicious or compromised MCP server can poison agent context and trigger unintended actions.
- **Apply least privilege.** Restrict file system access, network permissions, and tool availability to what the task actually requires. Don't give agents blanket access to production credentials or infrastructure.
- **Guard against approval fatigue.** Rapid code generation encourages rubber-stamping diffs. If you stop reading diffs, you stop catching bugs, vulnerabilities, and unwanted dependency additions. Slow down for security-critical paths.
- **Monitor agent-initiated changes.** Track file system modifications, dependency additions, network calls, and configuration changes made during agent sessions. Unexpected changes are a signal, not noise.
- **Include agent workflows in threat modeling.** Agents introduce new vectors: context poisoning (malicious data in fetched content), privilege escalation (agent runs commands you wouldn't), dependency confusion (agent adds unvetted packages).
- **Sandbox when possible.** Run agent tasks in containers, VMs, or restricted environments — especially for untrusted codebases or when testing agent-suggested commands.

## 22. Calibrate Review Depth to Risk

**Rationale:** Not all AI-generated code needs the same level of scrutiny. Treating every change with either blind trust or line-by-line paranoia wastes effort. A structured risk assessment lets you invest review effort where it matters most. — *Birgitta Böckeler, Thoughtworks; Anthropic*

- **Assess three dimensions before reviewing.** (1) Probability: how likely is the AI to get this wrong? (2) Impact: if it's wrong and undetected, what happens? (3) Detectability: will tests, types, or your familiarity catch mistakes?
- **Low probability + low impact + high detectability = light review.** Prototypes, internal tools, well-tested changes with typed languages — scan for obvious issues and move on.
- **High probability + high impact + low detectability = deep review.** Production code, unfamiliar domains, security-sensitive paths, missing test coverage — review as carefully as if you wrote it yourself.
- **Factor in context quality.** Is the codebase modular and well-named? Is the agent seeing the right files? Poor context increases probability of errors.
- **"Imagine you're on call."** Would you deploy this change tonight and sleep soundly? If not, increase your review depth.
- **Build intuition over time.** These assessments become second nature. The goal isn't a checklist — it's developing judgment for when to trust and when to verify.

## 23. Write for Autonomous Agents

**Rationale:** Interactive chat is only one mode. Increasingly, agents work asynchronously — picking up issues, executing in the background, and submitting results without real-time human guidance. Writing effective tasks for autonomous agents is a distinct and critical skill. — *Ellich & Etcovitch, GitHub; Mitchell Hashimoto*

- **Write issues as if for a newcomer.** The agent has no tribal knowledge. Include explicit context: what the feature does, where it lives in the codebase, and what patterns to follow.
- **Include examples of desired patterns.** Link to or paste similar implementations. "Follow the pattern in `src/handlers/userHandler.ts`" is worth more than a paragraph of description.
- **Make tasks atomic and self-contained.** Each task should be completable independently without requiring cross-task coordination. If a task has prerequisites, make them explicit.
- **Define done criteria in the task.** "Add a REST endpoint for /widgets that returns JSON, passes the existing integration test suite, and follows the error handling pattern in handlers/" is verifiable. "Improve the API" is not.
- **Leverage human strengths for human work.** Humans excel at ambiguity resolution, cross-system architectural decisions, and understanding *why*. Agents excel at tireless execution, repetitive transformations, and exploring parallel possibilities.
- **Provide custom instructions at the right scope.** Repository-level instructions for project conventions. Organization-level for cross-repo standards. Task-level for specific constraints.

## 24. Engineer Multi-Agent Systems Deliberately

**Rationale:** Multi-agent workflows — where agents hand off to other agents, share state, or coordinate actions — fail from the same causes as distributed systems: shared mutable state, implicit ordering assumptions, and unvalidated boundaries. Treat agent-to-agent interfaces with the same rigor as service-to-service APIs. — *Davis, GitHub Engineering*

- **Use typed schemas at every agent boundary.** Define the exact shape of data each agent produces and consumes. Treat schema violations as contract failures, not recoverable errors.
- **Constrain allowed actions.** Don't give agents open-ended capabilities. Define action schemas that enumerate exactly what each agent is allowed to do. Reject anything outside the schema.
- **Design for failure first.** Assume every agent call can fail, time out, or return garbage. Build retry logic, fallback paths, and circuit breakers before adding features.
- **Validate at boundaries, not after.** Check inputs before passing them to the next agent. Don't rely on downstream agents to handle bad upstream output.
- **Log intermediate state.** Capture what each agent received, decided, and produced. Without this, debugging multi-agent failures is nearly impossible.
- **Expect retries and partial failures.** Agents are non-deterministic. The same input may produce different outputs. Design for idempotency where possible.
- **Treat agents like distributed systems, not chat flows.** Apply the same engineering discipline: contract testing, observability, graceful degradation, and explicit failure handling.

## 25. Craft Agent-Computer Interfaces with Care

**Rationale:** Anthropic spent more time optimizing tool interfaces than overall prompts for their SWE-bench agent. The agent-computer interface (ACI) deserves the same design attention as human-computer interfaces. Poorly designed tools cause silent failures; well-designed ones make agents dramatically more capable. — *Anthropic, SWE-bench Engineering; Cursor, Agent Sandboxing*

- **Invest in tool descriptions like API docs.** Include usage examples, edge cases, input format requirements, and clear boundaries from similar tools. A good tool description reads like a docstring for a junior developer.
- **Error-proof tools (poka-yoke).** Require absolute paths instead of relative ones. Enforce unique matches for edits. Make it structurally hard for the agent to misuse the tool.
- **Surface constraints explicitly.** When an agent operates in a sandbox or restricted environment, describe those constraints in the tool description — not just in a rules file. Agents that know their boundaries before hitting them recover faster.
- **When tools fail, explain why specifically.** "Permission denied: sandbox blocks network access. Request escalation to proceed." is recoverable. "Error" is not. Specific failure messages reduce retry loops by 40%.
- **Keep formats natural.** Use formats close to what models saw in training (markdown, plain text). Avoid formats requiring counting (diff chunk headers) or heavy escaping (code inside JSON strings).
- **Test how agents actually use your tools.** Run many example inputs, observe failure modes, and iterate on descriptions. Tool design is empirical, not theoretical.

---

## Quick Reference

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
| 23 | Write for Autonomous Agents | Write tasks as if for a newcomer; atomic, self-contained, verifiable |
| 24 | Engineer Multi-Agent Systems | Typed schemas, constrained actions, design for failure, log everything |
| 25 | Craft Agent-Computer Interfaces | Error-proof tools, surface constraints, explain failures specifically |

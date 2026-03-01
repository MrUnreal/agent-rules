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

**Rationale:** Agents have finite context windows. Flooding the context with irrelevant information degrades output quality.

- **Stay focused on one task.** Finish the current task before starting a new one.
- **Reference specific files and functions** rather than vague descriptions. "Fix the `handleAuth` function in `src/auth.ts`" not "Fix the auth stuff."
- **Scope your searches.** Search in specific directories or file patterns rather than the entire codebase.
- **Summarize research findings** before acting on them. Don't carry raw search results through the entire session.
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

---

## Quick Reference

| # | Rule | One-Liner |
|---|------|-----------|
| 0 | Meta-Rule | Research → synthesize → write → validate → repeat |
| 1 | Explore First | Read the codebase before changing it |
| 2 | Plan First | Break tasks into steps before implementing |
| 3 | Verify Work | Test, lint, and confirm after every change |
| 4 | Small Steps | One logical change at a time |
| 5 | Manage Context | Stay focused, be specific, scope searches |
| 6 | Communicate | Ask when unclear, explain when acting |
| 7 | Quality Code | Follow conventions, handle errors, be explicit |
| 8 | Structured Workflows | Follow the right workflow for the task type |
| 9 | Delegate | Parallelize independent work, use subagents |
| 10 | Avoid Anti-Patterns | No kitchen sinks, no over-correction, no skipping failures |

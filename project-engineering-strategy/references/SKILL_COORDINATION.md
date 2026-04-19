# Skill Coordination

Use this reference when `project-engineering-strategy` overlaps with other skills or workflows.

## Precedence

Apply rules in this order:

1. Explicit user instruction
2. Project-local strategy mapping
3. `project-engineering-strategy`
4. Default habits of other skills

If another skill suggests a conflicting default, keep the higher-precedence rule.

## Coordination boundaries

### With `brainstorming`

- Use `brainstorming` for scope clarification, design shaping, solution comparison, and other design-first work before implementation.
- Keep `project-engineering-strategy` responsible for doc-root conventions, acceptance flow, handoff requirements, status language, and collaboration constraints.

### With `writing-plans`

- Use `project-engineering-strategy` to fix the collaboration model, artifact locations, WBS axis, acceptance flow, and status language.
- Use `writing-plans` only after that to turn an approved task or scope into an executable plan.
- Do not let plan structure override project-level strategy decisions that already exist.

### With `using-git-worktrees`

- Use `using-git-worktrees` for the technical mechanics of isolated work.
- Keep `project-engineering-strategy` as the authority for delivery paths, user-visible paths, and the sync-back threshold before review, acceptance, service launch, or formal commit/push.
- Do not present isolated worktree paths as final user-facing delivery paths.

### With `verification-before-completion`

- Use `project-engineering-strategy` to determine which artifacts and statuses must exist before a task is considered ready for human acceptance.
- Use `verification-before-completion` to enforce fresh verification evidence before any completion claim.

### With `systematic-debugging` and `test-driven-development`

- Use these skills for implementation and debugging method.
- Keep `project-engineering-strategy` responsible for document placement, acceptance evidence, handoff requirements, and tracker or issue synchronization.

### With `requesting-code-review`

- Use code review as a quality gate when that workflow is available.
- Review feedback does not override the strategy's acceptance fact source, status sync rules, or comment-source confirmation rules.

## Related-skill availability reminder

- Before leaning on another skill's workflow, check whether that skill is actually present in the current session's available skill list.
- If `brainstorming` is absent and the task is clearly design-first, give one short reminder that installing it is recommended for this workflow.
- Treat this as a soft reminder:
  - do not block the task
  - do not turn one missing skill into a long install checklist
  - do not keep repeating the same reminder every turn
- If the user chooses not to install the missing skill, continue with the current session and keep the limitation explicit only where it materially affects execution quality.

## Non-goals

- Do not use this skill to replace project-specific architecture design.
- Do not use this skill to replace implementation-specific debugging or test strategy.
- Do not turn this skill into a generic template dump for every possible workflow.

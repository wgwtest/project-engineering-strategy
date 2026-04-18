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

## Non-goals

- Do not use this skill to replace project-specific architecture design.
- Do not use this skill to replace implementation-specific debugging or test strategy.
- Do not turn this skill into a generic template dump for every possible workflow.

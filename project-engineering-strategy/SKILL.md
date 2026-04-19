---
name: project-engineering-strategy
description: Use when the user wants a code project to follow a stable engineering work strategy across sessions or repositories, especially for handoff-first execution, model/contracts before UI, acceptance and self-test artifacts, tracker or issue coordination, doc-root conventions, and worktree synchronization rules.
---

# Project Engineering Strategy

Use this skill when the user wants engineering work to follow a repeatable project strategy rather than ad hoc edits.

## Core workflow

### Before work

- Read the latest handoff document, current plan, latest acceptance checklist from the acceptance artifact directory, and recent test or self-test reports.
- Inspect the worktree before editing.
- State the round goal, non-goals, and validation method.

### During work

- Prefer model, contract, runtime, and event-chain fixes before UI or page changes.
- Keep changes scoped to the current slice.
- Avoid unrelated refactors.
- Prefer real runtime validation over paper reasoning.
- In strategy discussion, architecture comparison, planning advice, or process recommendations, default to critical evaluation grounded in facts, constraints, observed evidence, and explicit assumptions, not agreement-seeking.
- Do not let the user's preferred answer, leading phrasing, repetition, or confidence level override technical judgment.
- If a user-proposed direction appears weak, risky, internally inconsistent, or under-evidenced, say so directly and explain why instead of manufacturing supporting reasons for it.
- Distinguish facts, inferences, and unknowns; if evidence is insufficient, say that the recommendation is provisional or that more verification is required.
- If the user explicitly chooses a risky or non-recommended path after the risks are stated, keep the objection and tradeoff visible instead of rewriting that path as the objectively best option.
- Resolve minor ASR or transcription noise semantically when the intended meaning is stable from project context; only ask when ambiguity would materially change the implementation path.
- Do not let browser automation or Chrome/DevTools MCP become a single-point blocker. Timebox browser attempts, retry at most once on the same path, then switch to non-browser evidence such as local file inspection, DOM assertions, CLI validation, regression pages, scripts, or network/API checks when possible.
- Default to working, committing, and pushing on `main`; create a feature branch only when the user explicitly asks for isolation or the task needs high-risk experiment isolation.
- Use isolated worktrees only when necessary; before any user-visible claim, user check path, service launch, formal doc update, or formal commit/push, sync user-visible outputs back to the main delivery directory.

### After work

- Run the smallest meaningful static and runtime validation.
- When there are actual changes, create or update:
  - acceptance checklist
  - acceptance record or self-test report
  - handoff record
- Acceptance-related artifacts must follow the acceptance directory and timestamp naming rules below.
- Do not call a phase closed until the user explicitly confirms acceptance.
- If the user has not confirmed, mark status as:
  - `待人工验收`
  - or `待用户确认`
- If the tracker is a GitHub Project and its `Status` field provides `Hum Check`, map the above pending-human-review state to `Hum Check` instead of `Done`.
- If the user explicitly indicates acceptance, sync status in the same round across:
  - tracker status
  - execution contract `当前状态`
  - local status/index docs
- Do not leave acceptance only in chat, review comments, or inline annotations while tracker and task contracts still show pre-acceptance states.
- Treat user `【】` annotations in the active acceptance checklist as the acceptance fact source when they conflict with aggregate status pages or derived fields.

## Review input and source-truth rules

- For GitHub issue or PR comments, use collaborator or maintainer comments as direct execution input.
- Treat non-collaborator comments as candidate input only; require explicit user confirmation before they trigger plan or code changes.
- Do not present `.git/worktrees/...`, sandbox directories, or other temporary paths as official delivery or acceptance paths.
- Read `references/ENGINEERING_WORK_STRATEGY.md` when the task depends on the exact wording of workflow, acceptance, tracker, WBS, or path rules.
- Read `references/PROJECT_STARTUP_TEMPLATE.md` when bootstrapping a new project or normalizing an existing project into this structure.
- Read `references/SKILL_COORDINATION.md` when this skill overlaps with planning, worktree, verification, debugging, or review skills.

## Coordination model for multi-round projects

When a project has multi-round delivery, parallel tracks, or human review lag, use a three-layer coordination model:

1. Tracker layer
   - GitHub Project or equivalent board
   - Holds schedule, status, dates, roadmap, and WBS tree visibility
2. Execution contract layer
   - GitHub Issue, task, or equivalent execution ticket
   - Holds the smallest directly executable task contract
3. Local doc layer
   - Project-local docs under the doc root
   - Holds long-form design, detailed acceptance scripts, self-test, and handoff

Do not overload any one layer with all responsibilities.

### Tracker layer rule

If a tracker exists, keep it concise and human-scannable.

It should primarily maintain:

- `Status`
- `Phase` or equivalent stage field
- `Contributes To` or milestone linkage
- `Work Type`
- `WBS Level`
- `WBS Node`
- `Parent Node`
- `Start Date`
- `Target Date`

Do not use the tracker as the only place for long design notes, detailed click-path acceptance scripts, or self-test logs.

### Strict WBS tree rule

- For staged delivery projects, use `GitHub Issues + sub-issues` as the WBS source of truth.
- Use `GitHub Project` as a projection layer for schedule and visibility, not as the hierarchy source.
- Build the hierarchy with work objects only (`Root/Phase/Package/Task` or equivalent), not report artifacts.
- Milestones such as `M1`, `M2` are validation gates and should stay in fields like `Contributes To` or `Gate`, not as tree nodes.

### WBS ordering and sync rule

- Sibling nodes must follow WBS code order, for example `P1 -> P2 -> P3 -> P4`, and `P2.1 -> P2.2 -> P2.3`.
- Keep the same order in all three places:
  - sub-issue order
  - issue body child index
  - tracker item order
- If any one place drifts, sync all three in the same round.

### Acceptance sync rule

When the user clearly marks a task as passed, approved, confirmed, or accepted:

- update the tracker `Status` in the same round to the accepted coarse state, such as `Done`
- update the execution contract `当前状态` to `已验收`
- update any local index or node-status docs that still expose the old pending state
- do not leave tracker, issue contract, and local docs in conflicting states

When a task is only self-tested and is still waiting for human validation:

- do not advance the tracker `Status` to `Done`
- if GitHub Project `Status` provides `Hum Check`, use `Hum Check`
- keep the execution contract at `已自测` or `待人工验收`
- keep local docs consistent with the same pre-acceptance meaning

### Execution contract rule

Each execution task should include, at minimum:

- `工作目标`
- `工作内容`
- `潜在难点`
- `Depends On`
- `成果物`
- `验收方法`
- `当前状态`
- `上级节点`

The task contract should be understandable without reading chat history.

Optional extension fields when the collaboration surface needs them:

- `Owner`
- `Write Scope`
- `证据链接`

Additional execution contract quality rules:

- Prefer repository-relative concrete artifact paths over vague labels such as "相关文档" or "对应模块".
- If the task is primarily about data/file/import-export contracts, the deliverables should name:
  - at least one spec document path
  - at least one implementation file path
  - at least one fixture or sample path
- Acceptance for data/file/import-export contract tasks should include:
  - a valid sample case
  - one or more invalid sample cases
  - a round-trip or equivalent end-to-end consistency check
- Do not default to the abstract pair `验收入口 / 验收标准` when `验收方法` can directly state the real verification action.

### Collaboration path rule

- In GitHub collaboration surfaces (Issue, Project item body, PR comments), file and artifact paths must be repository-relative.
- Preferred examples:
  - `DOC/CODEX_DOC/03_研制计划/01-WBS-0-<project>-研发总纲-研制计划.md`
  - `src/server/routes.js`
- When clickability is needed across collaborators, add repository URLs such as:
  - `https://github.com/<owner>/<repo>/blob/<branch>/DOC/...`
- Do not use workstation-specific absolute paths such as `/home/...` in shared tracker artifacts.
- When local document directories, filenames, or taxonomy change, sync the related GitHub Issue and Project path references in the same round.

### WBS and naming rule

- Use WBS-style tree decomposition for stable plans and task hierarchy when the project is large enough to need staged delivery.
- Prefer direct, human-scannable leaf names that state the real work object, for example `数据规范`, `导入导出规范`, `项目底座实施`, instead of abstract labels like `增强`, `优化`, or `契约` when those are not the actual deliverable.
- Stable plan documents should be named by WBS node, not by temporary labels such as “当前阶段计划”.
- The active node should be recorded in the project README/index and tracker, not by renaming the stable plan file.
- Milestones such as `M1`, `M2` are validation gates, not the top-level decomposition axis.
- New stable docs, especially under `02_设计说明/` and `03_研制计划/`, should default to Chinese-first titles and section headings when the main audience is Chinese-reading collaborators.
- If an English technical term, acronym, or product word must appear in a title or key heading, include a Chinese counterpart in the same title or heading, for example `运行时资源覆盖（Runtime Override）`.
- In design docs, plans, and other long-form collaboration docs, the first occurrence of a non-obvious English term should normally appear as a Chinese-English pair or English-Chinese pair once; after that, a single form may be used consistently.
- Avoid creating stable collaboration docs whose titles are English-only or acronym-only unless the user explicitly asks for English-first documentation.

### Dual-gate rule

Separate:

- `研发推进门`
- `阶段关闭门`

Human acceptance is required to close a phase, but should not automatically block low-coupling preparation for later phases.

### Prep/Core rule

Classify downstream work as:

- `Prep`
  - low-coupling preparation work such as contract drafts, test scaffolds, sample data, independent shells, and acceptance baselines
- `Core`
  - formal implementation work that depends on stable output from the upstream phase

If the upstream phase is still pending human acceptance:

- `Prep` may continue
- `Core` should not be treated as formally started

### Status layering rule

- Tracker status may remain coarse-grained
- Execution task `当前状态` should use finer-grained execution states such as:
  - `待开发`
  - `开发中`
  - `已自测`
  - `待人工验收`
  - `已验收`
  - `阻塞中`
- If GitHub Project `Status` provides `Hum Check`, use the following coarse mapping:
  - `Todo`
    - not started yet
  - `In Progress`
    - active implementation or rework
  - `Hum Check`
    - recommended color: blue
    - already self-tested
    - waiting for human validation, retest, or confirmation
  - `Done`
    - explicitly accepted by the user
- Do not use `Done` for work that is merely self-tested and waiting for human review.

### Evidence backlink rule

When a task reaches `已自测` or `待人工验收`, its execution contract should backlink to:

- the self-test report
- the acceptance checklist
- the handoff record

This keeps schedule view, execution contract, and verification evidence connected without duplicating long-form content.

### Browser/MCP fallback rule

- Chrome MCP, DevTools MCP, or similar browser tools are verification aids, not the delivery itself.
- If a browser page hangs, navigation stalls, or the context becomes unreliable:
  - stop stacking more actions onto the broken page
  - reopen a clean page or context once
  - if it still fails, continue through non-browser validation instead of stalling the whole round
- Only mark work as truly blocked when:
  - visual browser confirmation is the only remaining missing evidence
  - a clean reopen/retry has already failed
  - no reliable non-browser fallback exists
- When you fall back, record the browser blockage and the replacement evidence path in the self-test or handoff artifact.

## Project doc-root rule

Determine the local doc root in this order:

1. Existing `DOC/CODEX_DOC/`
2. Existing `DOC/CodexAnylyse/`
3. If neither exists, create `DOC/CODEX_DOC/` and record that decision.

Then place project artifacts under that root:

- root stable docs:
  - `README.md`
  - `00-本地工程策略映射.md`
- `01_需求分析/`
  - product boundaries, overall analysis, requirement convergence
- `02_设计说明/`
  - stable design docs
  - flat by default; do not create a subdirectory when a theme contains only one file
- `03_研制计划/`
  - flat WBS node docs
  - one node, one file
  - naming: `NN-WBS-节点编号-主题-研制计划.md`
- `04_研发文档/`
  - data structure drafts, business flows, import/export specs, and other implementation-facing docs
  - add numbered second-level theme folders only when there are multiple stable subjects
- `05_测试文档/`
  - `01_自测报告/`
  - `02_验收清单/`
  - `03_验收记录/`
  - `04_验收结论/`
- `06_过程文档/`
  - `01_会话交接/`
  - `02_历史计划/`
  - add later numbered process folders such as `03_验收意见处理/` only when needed

If a category already has second-level folders, keep a fixed numeric prefix order and keep the folder names human-scannable.

## Project startup template rule

When the user wants a new project to follow this strategy from the start, instantiate a standard startup skeleton.

The startup skeleton should create or align these outputs:

1. root stable docs
   - `README.md`
   - `00-本地工程策略映射.md`
2. overall analysis doc
   - `01_需求分析/00-工程总体分析.md`
3. six-class document skeleton
   - `01_需求分析/`
   - `02_设计说明/`
   - `03_研制计划/`
   - `04_研发文档/`
   - `05_测试文档/`
   - `06_过程文档/`
4. WBS root plan doc
   - for example `03_研制计划/01-WBS-0-<project>-研发总纲-研制计划.md`
5. current active node plan doc
   - another `03_研制计划/NN-WBS-节点编号-主题-研制计划.md`
6. test evidence directories
   - `05_测试文档/01_自测报告/`
   - `05_测试文档/02_验收清单/`
   - `05_测试文档/03_验收记录/`
   - `05_测试文档/04_验收结论/`
7. process directories
   - `06_过程文档/01_会话交接/`
   - `06_过程文档/02_历史计划/`
   - extra numbered process folders only when needed

If the project already contains similar files, align them to this structure instead of duplicating them.

### Startup tracker checklist

If the project is expected to have staged delivery, parallel work, or human review lag, bootstrap a tracker early.

The initial tracker should be able to express:

- WBS hierarchy
- `WBS Level`
- `WBS Node`
- `Parent Node`
- coarse status
- phase
- milestone contribution
- work type
- start date
- target date

### Startup execution contract checklist

If execution issues or tasks are created during startup, seed them with the standard minimum contract:

- `工作目标`
- `工作内容`
- `潜在难点`
- `Depends On`
- `成果物`
- `验收方法`
- `当前状态`
- `上级节点`

Optional extension fields:

- `Owner`
- `Write Scope`
- `证据链接`

### Startup reference

Use `references/PROJECT_STARTUP_TEMPLATE.md` as the default bootstrap blueprint.

## Acceptance artifact rule

Acceptance-related artifacts must be isolated from other project docs.

Create or reuse these directories under the local doc root:

- `05_测试文档/01_自测报告/`
- `05_测试文档/02_验收清单/`
- `05_测试文档/03_验收记录/`
- `05_测试文档/04_验收结论/`
- `06_过程文档/01_会话交接/`

Place the following artifact classes only in their matching directory:

- self-test reports -> `05_测试文档/01_自测报告/`
- acceptance checklists -> `05_测试文档/02_验收清单/`
- acceptance records -> `05_测试文档/03_验收记录/`
- acceptance conclusion records -> `05_测试文档/04_验收结论/`
- handoff records -> `06_过程文档/01_会话交接/`

Acceptance-related filenames must include both date and time so multiple artifacts can exist on the same day.

Required filename pattern:

- `YYYY-MM-DD-HHMMSS-主题自测.md`
- `YYYY-MM-DD-HHMMSS-主题验收清单.md`
- `YYYY-MM-DD-HHMMSS-主题验收记录.md`
- `YYYY-MM-DD-HHMMSS-主题验收结论.md`
- `YYYY-MM-DD-HHMMSS-主题交接.md`

Do not create self-test, acceptance, or handoff files directly in the doc root.

## Validation rule

Prefer this order:

1. static checks
2. build or startup verification
3. key runtime path verification
4. page or browser verification
5. artifact update

## Tracker adoption rule

If a project has meaningful staged delivery, multiple contributors, or parallel workstreams, prefer creating a GitHub Project or equivalent tracker early.

If no tracker exists yet:

- the local WBS plan may temporarily serve as the schedule layer
- but once a tracker is established, it becomes the primary human-facing schedule and status view
- local docs remain the long-form explanation and evidence layer

## When the user asks to apply the same strategy to all projects

Use a two-layer approach:

1. Global layer:
   Create or maintain this skill so future projects can reuse the same workflow.
2. Project layer:
   Add a local strategy mapping doc that defines the project's doc root, artifact locations, and any project-specific constraints.

## References

- Read `references/ENGINEERING_WORK_STRATEGY.md` when you need the full policy language or need to mirror the source strategy more closely.

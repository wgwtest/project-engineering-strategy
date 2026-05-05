---
name: project-engineering-strategy
description: Use when the user wants a code project to follow a stable engineering work strategy across sessions or repositories, especially for handoff-first execution, model/contracts before UI, prototype package governance, prototype-based visual acceptance, tracker or issue coordination, doc-root conventions, and worktree synchronization rules.
---

# Project Engineering Strategy

Use this skill when the user wants engineering work to follow a repeatable project strategy rather than ad hoc edits.

## Mother model rule

Treat the canonical strategy as a 12-section mother model. By default, sections `1-9` use the same six-part structure:

- `目标与边界`
- `事实源`
- `强制执行门`
- `同步义务`
- `例外或降级规则`
- `产物与证据`

The current mother-model chapters are:

1. `本地文档治理`
2. `远端协作与工程跟踪治理（Tracker）`
3. `WBS 与计划治理`
4. `任务执行约定治理`
5. `状态机与关闭门`
6. `主目录与隔离工作区治理（Worktree）`
7. `事实源判定与同步治理`
8. `验证、验收与证据治理`
9. `会话交接与多轮协同`
10. `架构治理`
11. `改动边界与兼容风险`
12. `版本发布与对外导出`

The exception chapters are:

- `架构治理`
- `改动边界与兼容风险`
- `版本发布与对外导出`

## Related skill availability reminder

- Before relying on another skill's workflow, check the current session's available skill list.
- If a clearly related skill is missing and the current task would normally benefit from it, give one short install suggestion before continuing.
- Treat this as a soft reminder, not a blocking gate.
- First-priority reminder target:
  - `brainstorming`
    - remind only when the task is mainly about scoping, design shaping, requirements clarification, solution comparison, or other design-first work
    - the reminder should say that the current session does not expose `brainstorming`, that this strategy usually works better with it for design-first work, and that the user may want to install it
- Do not turn this into a generic "install more skills" prompt.
- Do not recommend loosely related skills just because they exist.
- Do not repeat the same reminder every turn unless the task context materially changes.
- If the user does not act on the reminder, continue with best-effort execution and keep the missing-skill limitation visible when it matters.

## Core workflow

### Before work

- If the repository root contains a Codex/session startup guide such as `CODEX_START_HERE.md`, read it before other project files and treat it as the fast recovery entry; if it conflicts with stable formal docs, the formal doc root still wins.
- Read the latest handoff document, current plan, the current acceptance main entry and current node acceptance method, and recent machine-test records or equivalent recent test evidence.
- Inspect the worktree before editing.
- State the round goal, non-goals, and validation method.
- For UI or page work, determine whether a design, mockup, sample, prototype image, HTML prototype, or approved visual effect exists; if yes, name it as an implementation fact source before coding.
- For prototype creation, prototype refresh, or prototype-driven UI work, read `references/PROTOTYPE_PACKAGE_STANDARD.md` and determine the formal prototype root before creating files.
- If the task involves requirement-specification authoring or revising a formal requirement-specification document, first identify:
  - the current stable main spec document,
  - whether this round needs a separate supplement document,
  - the target chapter structure to preserve,
  - and the user-review gate before writing accepted content back into the main spec.

### During work

- Prefer model, contract, runtime, and event-chain fixes before UI or page changes.
- Keep changes scoped to the current slice.
- Avoid unrelated refactors.
- Prefer real runtime validation over paper reasoning.
- For requirement-specification work, preserve a stable chaptered main document rather than turning the spec into ad hoc notes, raw Q&A transcripts, or patch-only fragments.
- When a requirement-specification change is structurally meaningful, default to a two-step flow:
  1. write a supplement/supplement-plan document for review,
  2. after user approval, write the accepted result back into the main spec document.
- If a page has an approved design/prototype/effect image, treat it as part of the implementation standard, not as optional inspiration; do not replace screenshot comparison with subjective judgment or old runtime-page continuation.
- If creating or revising a prototype, create a versioned prototype package instead of loose images; every review image must have a written design basis in the package README.
- Do not overwrite a reviewed prototype version for a new direction or material revision; create the next version folder and preserve or archive the previous version according to the prototype package rules.
- Before changing GitHub Project, GitLab boards, or another remote collaboration surface, first confirm that the surface is formally adopted and that schema mutation is allowed in this round.
- In strategy discussion, architecture comparison, planning advice, or process recommendations, default to critical evaluation grounded in facts, constraints, observed evidence, and explicit assumptions, not agreement-seeking.
- Do not let the user's preferred answer, leading phrasing, repetition, or confidence level override technical judgment.
- If a user-proposed direction appears weak, risky, internally inconsistent, or under-evidenced, say so directly and explain why instead of manufacturing supporting reasons for it.
- Distinguish facts, inferences, and unknowns; if evidence is insufficient, say that the recommendation is provisional or that more verification is required.
- If the user explicitly chooses a risky or non-recommended path after the risks are stated, keep the objection and tradeoff visible instead of rewriting that path as the objectively best option.
- Resolve minor ASR or transcription noise semantically when the intended meaning is stable from project context; only ask when ambiguity would materially change the implementation path.
- Do not let browser automation or Chrome/DevTools MCP become a single-point blocker. Timebox browser attempts, retry at most once on the same path, then switch to non-browser evidence such as local file inspection, DOM assertions, CLI validation, regression pages, scripts, or network/API checks when possible.
- Default to working, committing, and pushing on `main`; create a feature branch only when the user explicitly asks for isolation or the task needs high-risk experiment isolation.
- Use isolated worktrees only when necessary; before any user-visible claim, user check path, service launch, formal doc update, or formal commit/push, sync user-visible outputs back to the main delivery directory.
- For GitHub public skill releases, do not treat pushed tags as published releases by themselves; create the GitHub Release and verify the anonymous `releases/latest` API before reporting publication.

### After work

- Run the smallest meaningful static and runtime validation.
- For UI or page work with an approved design/prototype/effect image, produce prototype screenshot + runtime screenshot + comparison conclusion before claiming completion or asking for acceptance.
- For newly generated prototypes, verify source files, rendered images, README design-basis coverage, and regeneration commands before asking for human review.
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
- Read `references/PROTOTYPE_PACKAGE_STANDARD.md` when creating, moving, refreshing, reviewing, or implementing against prototype images, HTML prototypes, design screenshots, canvas mockups, or effect images.
- Read `references/SKILL_COORDINATION.md` when this skill overlaps with planning, worktree, verification, debugging, or review skills.
- For public release tasks, prefer the repository release script when available, and report tag push, GitHub Release creation, and public latest visibility as separate facts.

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

### Remote tracker governance rule

- When a project exposes GitHub Project, GitLab boards, or another writable remote tracker, first determine whether that surface is formally adopted as the project's tracker layer.
- Visibility is not permission. Seeing a board does not mean you should mutate it.
- Before creating or changing remote tracker schema, explicitly confirm that the user allows remote-tool use and schema mutation for this project.
- Schema mutation includes fields, status options, groupings, views, automations, and other structural changes that affect collaborators.
- Without that approval, you may read existing tracker state but must not create, rename, delete, or repurpose remote fields or status options.
- If no remote tracker has been formally adopted yet, keep schedule and execution detail in local docs until the project chooses one.

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
  - `DOC/CODEX_DOC/04_研制计划/01-WBS-0-<project>-研发总纲-研制计划.md`
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
- New stable docs, especially under `02_设计说明/` and `04_研制计划/`, should default to Chinese-first titles and section headings when the main audience is Chinese-reading collaborators.
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
- If remote schema changes are allowed, prefer a dual-layer model:
  - keep `Status` coarse-grained for schedule and roadmap readability
  - add `Execution Status` or `当前状态` as a separate field for the fine-grained states above
- Only collapse the fine-grained states directly into the remote `Status` field when:
  - the user explicitly wants a single-field model
  - the tool cannot support a second status-like field cleanly
  - or the existing project already depends on that single-field model and preserving continuity is cheaper than migration
- If you choose the single-field model, keep the tradeoff visible: roadmap readability and execution detail become coupled.

### Evidence backlink rule

When a task reaches `已自测` or `待人工验收`, its execution contract should backlink to:

- the self-test report
- the acceptance checklist
- the handoff record
- for prototype-backed UI work, the screenshot comparison record

This keeps schedule view, execution contract, and verification evidence connected without duplicating long-form content.

### Prototype visual acceptance rule

For any page or UI feature with an existing design draft, sample image, static prototype, HTML prototype, or approved effect screenshot:

- The design/prototype is an implementation standard and must be named in the plan, task contract, or handoff.
- Before coding, record the source artifact, target route, page owner/app, main business object, allowed deviations, and unacceptable deviations.
- Before completion, capture the real runtime page from a running system and compare it with the source design/prototype.
- Required evidence is: source prototype screenshot, runtime screenshot, and a written comparison conclusion.
- Passing automated tests, type checks, builds, route `200 OK`, or verbal “looks close” claims are not substitutes for screenshot comparison.
- Minor differences in real data, image assets, font rendering, local spacing, and color brightness may pass; page structure, core blocks, action entry points, visual hierarchy, and object semantics must match.
- If browser automation fails, timebox and retry once; if still blocked, record the blockage and provide the strongest available fallback evidence, but do not call visual acceptance complete unless reliable visual evidence exists.

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
    - must explicitly state the documentation-governance basis
    - must name the absorbed standard-control families
    - must state whether the project also has a standard-projection layer
- `01_需求分析/`
  - product boundaries, overall analysis, requirement convergence
- `02_设计说明/`
  - stable design docs
  - flat by default; do not create a subdirectory when a theme contains only one file
  - for requirement-specification main docs, prefer one stable main document plus dated supplement docs for major structured revisions
- `03_规范与流程/`
  - shared data specs, key flows, design-implementation mapping, and other long-lived cross-node rules
  - add numbered second-level theme folders only when there are multiple stable subjects
- `04_研制计划/`
  - flat WBS node docs
  - one node, one file
  - naming: `NN-WBS-节点编号-主题-研制计划.md`
- `05_节点合同/`
  - one node, one execution contract when the project uses local WBS-node contracts
  - naming: `NN(.NN)-节点编号-主题-节点合同.md`
- `06_测试文档/`
  - `01_验收大纲/`
  - `02_验收入口/`
  - `03_机测记录/`
  - `04_人测记录/`
  - `05_验收结论/`
- `07_过程文档/`
  - `01_会话交接/`
  - `02_历史计划/`
  - add later numbered process folders such as `03_验收意见处理/` only when needed

If a category already has second-level folders, keep a fixed numeric prefix order and keep the folder names human-scannable.

## Requirement-specification governance rule

For requirement-specification work, treat the formal spec as a stable downstream-facing artifact rather than a disposable working note.

Default structure expectations for the main requirement-specification document:

- purpose, scope, writing stance, and terminology rules
- system positioning, business goals, overall architecture understanding, and phase positioning
- overall layering, module map, and inter-module boundaries
- roles, business objects, object relationships, behaviors, constraints, and state changes
- key flows, rules, boundaries, and non-goals
- if the system has backend/frontend or multi-surface collaboration, separate the structure explicitly:
  - backend stack, layering principles, module overview, and per-module responsibilities
  - frontend stack, layering principles, page/workspace map, view-model boundaries, load lifecycle, and state-machine design
- for each key submodule, describe:
  - purpose
  - inputs/outputs
  - internal subparts
  - interfaces or commands
  - key states and failure handling
  - collaboration with neighbor modules
- completion, checking, and freeze criteria
- formal outputs consumed by downstream stages and their handoff constraints

Default process expectations for meaningful revisions:

1. create a separate supplement document first
2. describe why the revision is needed and which chapters will change
3. get user review on that supplement direction
4. write accepted results back into the main spec
5. keep the supplement as process evidence, not as the long-term substitute for the main spec

## Codex startup guide rule

For multi-worktree or multi-session projects, create or maintain a short repository-root startup guide for new Codex sessions, normally named `CODEX_START_HERE.md`.

The guide should summarize:

- project purpose and current facts of source
- required reading order
- main directory vs worktree rules
- major subsystem map
- service startup and verification commands
- commit, runtime-data, and handoff constraints

Governance rules:

- Keep one canonical guide in the main delivery directory instead of divergent per-worktree copies.
- Commit the guide on `main` and sync it into active worktrees by rebasing or merging from `main`.
- Do not overwrite active worktree changes while distributing the guide; stash/pop or commit local work first.
- Update the guide when stable project entry points, branch/worktree policy, subsystem boundaries, startup commands, or validation commands change.
- The guide is a fast recovery entry, not a replacement for `DOC/CODEX_DOC/` or the latest handoff and acceptance records.

## Project startup template rule

When the user wants a new project to follow this strategy from the start, instantiate a standard startup skeleton.

The startup skeleton should create or align these outputs:

1. root stable docs
   - repository-root startup guide, for example `CODEX_START_HERE.md`, when the project has repeated Codex sessions or active worktrees
   - `README.md`
   - `00-本地工程策略映射.md`
     - include the documentation-governance basis
     - include the standard-boundary statement
2. overall analysis doc
   - `01_需求分析/00-工程总体分析.md`
3. seven-class document skeleton
   - `01_需求分析/`
   - `02_设计说明/`
   - `03_规范与流程/`
   - `04_研制计划/`
   - `05_节点合同/`
   - `06_测试文档/`
   - `07_过程文档/`
4. WBS root plan doc
   - for example `04_研制计划/01-WBS-0-<project>-研发总纲-研制计划.md`
5. current active node plan doc
   - another `04_研制计划/NN-WBS-节点编号-主题-研制计划.md`
6. current active node contract doc when local node contracts are enabled
   - for example `05_节点合同/NN-WBS-节点编号-主题-节点合同.md`
7. test evidence directories
   - `06_测试文档/01_验收大纲/`
   - `06_测试文档/02_验收入口/`
   - `06_测试文档/03_机测记录/`
   - `06_测试文档/04_人测记录/`
   - `06_测试文档/05_验收结论/`
8. process directories
   - `07_过程文档/01_会话交接/`
   - `07_过程文档/02_历史计划/`
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

- `06_测试文档/01_验收大纲/`
- `06_测试文档/02_验收入口/`
- `06_测试文档/03_机测记录/`
- `06_测试文档/04_人测记录/`
- `06_测试文档/05_验收结论/`
- `07_过程文档/01_会话交接/`

Place the following artifact classes only in their matching directory:

- acceptance outlines -> `06_测试文档/01_验收大纲/`
- acceptance main entry and methods -> `06_测试文档/02_验收入口/`
- machine-test records -> `06_测试文档/03_机测记录/`
- human-test records -> `06_测试文档/04_人测记录/`
- acceptance conclusion records -> `06_测试文档/05_验收结论/`
- handoff records -> `07_过程文档/01_会话交接/`

The acceptance entry layer is not the executable document itself. `00-验收主入口.md` is the user-facing access file, while `验收方法` is the executable, annotatable document that may also serve as the human-acceptance fact source for the current round.

Timestamp-first naming is required for machine-test, human-test, acceptance-conclusion, and handoff files so multiple artifacts can exist on the same day.

Required filename pattern:

- `YYYY-MM-DD-HHMMSS-主题-机测记录.md`
- `00-验收主入口.md`
- `<WBS编码>-主题-验收方法.md`
- `SETTING-范围名-验收方法.md`
- `YYYY-MM-DD-HHMMSS-主题-人测记录.md`
- `YYYY-MM-DD-HHMMSS-主题验收结论.md`
- `YYYY-MM-DD-HHMMSS-主题交接.md`

Do not create machine-test, acceptance, or handoff files directly in the doc root.

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

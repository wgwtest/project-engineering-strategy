# Engineering Work Strategy

## 1. Goal

Use this reference as a reusable engineering workflow baseline for software projects that need:

1. stable execution across multiple sessions
2. explicit handoff and recovery points
3. separation between self-test evidence and human acceptance
4. predictable document and task structure
5. safe coordination between main delivery directories and isolated worktrees

The intent is not to force one toolchain on every project. The intent is to keep project truth recoverable, reviewable, and synchronized across code, docs, and collaboration surfaces.

## 2. Core principles

### 2.1 Understand before editing

- Read the current plan, relevant design material, latest handoff, and recent acceptance or self-test artifacts before changing code.
- Confirm the target boundary, current implementation status, open risks, and non-goals before broad edits.
- Do not make large changes while the execution context is still incomplete.

### 2.2 Stabilize models and contracts before UI

- Prefer fixing shared models, data structures, contracts, and event semantics before UI or page-level polish.
- Push logic and contract clarity ahead of presentation changes.
- Do not let temporary display requirements hard-code cross-module behavior.

### 2.3 Work in small slices and keep the system runnable

- Advance one clear slice at a time.
- Avoid parallel expansion across multiple high-risk targets in the same round unless the work is truly decoupled.
- After each round, keep the system buildable, inspectable, or otherwise verifiable.

### 2.4 Prefer real effect over superficial completion

- Prioritize changes that affect real outputs, real flows, and real runtime behavior.
- If a capability is described as supported, make sure it affects at least one real path.
- Prefer runtime evidence over paper reasoning.

### 2.5 Keep docs synchronized with code and status

- Record design changes, scope changes, round conclusions, acceptance outcomes, and handoff state in project artifacts.
- Do not leave project truth only in chat.
- Make each round recoverable from files, not memory.

### 2.6 Resolve minor transcription noise semantically

- User input may contain ASR or transcription noise.
- If the intended meaning is stable from project context, proceed with the corrected semantic interpretation.
- Only ask when ambiguity would materially change the implementation path.

## 3. Standard workflow

### 3.1 Before work

- Read the latest handoff document.
- Read the current plan and current execution contract.
- Read the latest acceptance checklist and recent self-test record when they exist.
- Inspect the worktree before editing.
- State the round goal, non-goals, and validation method.

### 3.2 During work

- Find the smallest meaningful entry point before editing.
- Prefer new focused modules or files over repeatedly expanding an already overloaded file.
- For complex changes, stabilize the abstraction layer before wiring business behavior.
- Be cautious around existing user changes, project configuration, and generated artifacts.
- Default to working on `main`; create an isolated branch or worktree only when the user asks for isolation or the task truly needs high-risk experimentation.

### 3.2A Delivery paths and worktree synchronization

To avoid “changed in an isolated directory, reviewed in another directory” failures, make these path roles explicit:

1. `repository main directory`
   - the official working tree for `git status`, `git commit`, and `git push`
2. `user review directory`
   - the directory the user actually opens for reading files, running the app, or performing human acceptance
3. `isolated worktree`
   - a temporary internal directory for high-risk experiments, conflict isolation, or parallel low-sharing work

Rules:

- User-facing delivery paths should point only to the repository main directory or the user review directory.
- Do not present `.git/worktrees/...`, temporary sandboxes, or tool-private directories as official delivery or acceptance paths.
- If an output exists only in an isolated worktree, it is not yet in a deliverable or reviewable state.

Use isolated worktrees only when:

- the user explicitly asks for isolation
- the work is high risk and unsafe to perform directly in the main tree
- multiple low-sharing tasks must run in parallel

Even when isolated worktrees are used, the final delivery location stays the main delivery directory.

Sync isolated worktree outputs back before any of these moments:

1. before the user opens files for review
2. before human acceptance starts
3. before claiming “done”, “fixed”, or “ready to test”
4. before launching a local service for user verification
5. before updating formal plans, design docs, self-test, acceptance, or handoff docs
6. before formal `git commit` or `git push`
7. before ending a round that has already produced user-visible output

Unsynced isolated outputs:

- must not be described as formally delivered
- must not be used as the user annotation path
- must not overwrite shared status references as though the main tree already matched them

### 3.3 After work

- Run the smallest meaningful static or runtime validation.
- When there are real changes, create or update:
  - self-test record or acceptance record
  - acceptance checklist
  - handoff record
- Treat the round as `待人工验收` or `待用户确认` until the user explicitly confirms acceptance.
- Do not describe a phase as closed before human acceptance is explicit.

### 3.4 When acceptance feedback arrives

- Read the latest active acceptance checklist first.
- Treat only user content inside `【】` in the active checklist as formal acceptance input.
- Do not treat developer-maintained fields such as `状态`, `验收结论`, or placeholder checkboxes as human judgment.
- Aggregate pages, README indices, issue bodies, and project status boards are derived surfaces, not fact sources.
- If user feedback requires interpretation, create a dedicated acceptance-feedback handling document before changing plans or code.
- Keep human acceptance checklists limited to user-observable actions and document verification actions; do not outsource developer self-test commands into the human checklist.

### 3.5 Review input and source triage

When using GitHub issue or pull-request comments as input:

1. collaborator or maintainer comments may be used as direct execution input
2. non-collaborator comments are candidate input only

For non-collaborator comments:

- record the source class and current conclusion
- do not let them directly trigger plan or code changes
- require explicit user confirmation before execution

If a non-collaborator comment conflicts with the active acceptance checklist, the active checklist `【】` content remains the current fact source until the user says otherwise.

## 4. Three-layer coordination model

When a project has staged delivery, parallel tracks, or delayed human review, separate collaboration into three layers:

1. `Tracker`
   - schedule, phase, coarse status, roadmap, WBS visibility
2. `Execution contract`
   - the smallest directly executable task contract
3. `Local docs`
   - long-form design, self-test, acceptance scripts, acceptance records, handoff, and process archives

Do not overload one layer with every responsibility.

### 4.1 Tracker rules

- Keep tracker items concise and human-scannable.
- Recommended fields:
  - `Status`
  - `Phase`
  - `Contributes To`
  - `Work Type`
  - `WBS Level`
  - `WBS Node`
  - `Parent Node`
  - `Start Date`
  - `Target Date`
- Do not use the tracker as the only place for detailed design notes, long acceptance scripts, or self-test logs.

### 4.2 Execution contract rules

Each executable task should include at least:

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

Quality rules:

- Prefer repository-relative concrete paths over vague labels.
- For data or import/export work, name at least one spec path, one implementation path, and one fixture or sample path.
- Acceptance for data or import/export work should include a valid sample case, invalid sample cases, and a round-trip or end-to-end consistency check when applicable.

### 4.3 Local document rules

Use the local doc layer for:

- requirement convergence
- stable design docs
- WBS plans
- implementation-facing specs
- self-test and acceptance artifacts
- handoff and process archives

## 5. WBS and naming rules

- Use WBS-style tree decomposition when the project is large enough to need staged delivery.
- Use work objects as tree nodes, not report artifacts.
- Use milestones such as `M1`, `M2`, and `M3` as validation gates, not as the top-level decomposition axis.
- Sibling nodes should follow WBS order, and the same order should stay aligned across tracker order, issue order, and local plan order.
- Name stable plan documents by WBS node, not by temporary labels such as “current plan”.
- Record the active node in the README or tracker rather than renaming stable files every round.

## 6. Status layering and evidence links

- Tracker status may stay coarse.
- Execution contracts should use finer-grained states such as:
  - `待开发`
  - `开发中`
  - `已自测`
  - `待人工验收`
  - `已验收`
  - `阻塞中`

When a task reaches `已自测` or `待人工验收`, its execution contract should backlink to:

- the self-test report
- the acceptance checklist
- the handoff record

If the tracker uses a coarse single-select field, a common mapping is:

- `Todo`
- `In Progress`
- `Hum Check`
- `Done`

But the exact coarse labels matter less than keeping them synchronized with the finer execution status.

## 7. Collaboration path rules

- In GitHub issues, project items, and pull-request comments, use repository-relative paths by default.
- If collaborators need clickable links, add repository URLs.
- Do not place workstation-specific absolute paths such as `/home/...` in shared collaboration surfaces.

## 8. Recommended doc-root structure

If the project already has a stable formal doc root, keep it.

If it does not, create:

- `DOC/CODEX_DOC/`

Recommended structure:

- root stable docs
  - `README.md`
  - `00-本地工程策略映射.md`
- `01_需求分析/`
- `02_设计说明/`
- `03_研制计划/`
- `04_研发文档/`
- `05_测试文档/`
  - `01_自测报告/`
  - `02_验收清单/`
  - `03_验收记录/`
  - `04_验收结论/`
- `06_过程文档/`
  - `01_会话交接/`
  - `02_历史计划/`
  - add later numbered process folders only when needed

Document naming recommendations:

- WBS plans: `NN-WBS-节点编号-主题-研制计划.md`
- self-test: `YYYY-MM-DD-HHMMSS-主题自测.md`
- acceptance checklist: `YYYY-MM-DD-HHMMSS-主题验收清单.md`
- acceptance record: `YYYY-MM-DD-HHMMSS-主题验收记录.md`
- acceptance conclusion: `YYYY-MM-DD-HHMMSS-主题验收结论.md`
- acceptance-feedback handling: `YYYY-MM-DD-HHMMSS-主题验收意见处理.md`

## 9. Acceptance fact-source rules

Make these definitions explicit:

- `active checklist`
  - the current formal human-acceptance entry for a node
- `fact source`
  - user `【】` content in the active checklist
- `derived surfaces`
  - file-name status tags
  - acceptance index pages
  - tracker status
  - issue body status fields
  - README summaries

If they conflict, the active checklist `【】` content wins.

Common synchronization rule:

- if the user explicitly writes `【通过】` or an equivalent acceptance phrase, synchronize:
  - acceptance checklist state
  - issue `当前状态`
  - tracker `Status`
  - local acceptance indices
- if the user has not explicitly accepted, keep the task in a pending human-review state

## 10. Handoff rules

Every handoff should answer at least four questions:

1. what was the round goal
2. what is already finished
3. what remains unfinished
4. where the next round should resume

Handoffs should include:

- concrete paths
- relevant files
- commands when needed
- a suggested next-step order

When a new acceptance checklist exists, the handoff should link it explicitly.

When acceptance feedback already exists, the handoff should also link the acceptance-feedback handling document.

## 11. Quick operating directives

- Read docs before code.
- Stabilize contracts before implementation.
- Prefer backend or runtime truth before page polish.
- Advance in small slices.
- Prefer real effect over superficial completion.
- Keep status and docs synchronized.
- Verify before claiming completion.
- Leave the next round a recoverable handoff.

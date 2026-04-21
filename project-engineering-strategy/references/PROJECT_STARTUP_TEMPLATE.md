# Project Startup Template

Use this template when a project should adopt the engineering strategy from the beginning, or when an existing project needs to be normalized into the same structure.

## 1. Goal

Bootstrap a project so that:

1. the plan structure is stable
2. the execution contract is explicit
3. the acceptance and handoff evidence has a fixed home
4. schedule view and long-form documentation are separated
5. document categories and naming stay consistent across projects

## 2. Startup outputs

Create or align the following outputs under the project-local doc root.

### 2.1 Root stable docs

1. `README.md`
   - active WBS node
   - reading order
   - collaboration rules
   - roadmap location
2. `00-本地工程策略映射.md`
   - local doc root decision
   - documentation-governance basis
   - standard-boundary statement
   - tracker URL or tool location
   - issue contract policy
   - project-specific constraints
3. `01_需求分析/00-工程总体分析.md`
   - current structure
   - module decomposition
   - current gaps and risks

### 2.2 Numbered document taxonomy

Create or align:

1. `01_需求分析/`
2. `02_设计说明/`
3. `03_规范与流程/`
4. `04_研制计划/`
5. `05_节点合同/`
6. `06_测试文档/`
7. `07_过程文档/`

Rules:

1. `02_设计说明/` stores design正文 directly by default; do not create a subdirectory when a theme has only one file.
2. `03_规范与流程/` stores shared specs, key flows, and mapping docs that cannot be reduced to a single node.
3. `04_研制计划/` stores WBS node docs flatly; one node keeps one file.
4. `04_研制计划/` files use: `NN-WBS-节点编号-主题-研制计划.md`.
5. `05_节点合同/` stores single-node execution contracts when the project adopts local node contracts.
6. `05_节点合同/` files use: `NN(.NN)-节点编号-主题-节点合同.md`.
7. If a category needs second-level folders, those folders also use stable numeric prefixes.
8. For Chinese-reading teams, new stable doc titles and major headings should default to Chinese-first wording.
9. If a title must contain an English technical term, acronym, or product word, add the Chinese counterpart in the same title or main heading at least once.

### 2.2A Documentation-governance basis

Every project that adopts this strategy must record its documentation-governance basis in `00-本地工程策略映射.md`.

At minimum, write:

1. which standard-control families are being absorbed
   - recommended default set:
     - `ISO/IEC/IEEE 12207`
     - `ISO/IEC/IEEE 15289`
     - `ISO/IEC/IEEE 16326`
     - `ISO/IEC/IEEE 29148`
     - `ISO/IEC/IEEE 29119`
     - `IEEE 1016`
2. whether the local doc root is:
   - the project's R&D-layer formal doc root
   - or a direct standard-delivery package
3. whether the project also maintains a standard-projection layer
   - for example an industry, customer, or defense-delivery projection layer
4. which local extension doc classes are enabled
   - for example `05_节点合同/`, `06_测试文档/02_验收大纲/`, `06_测试文档/05_验收清单/`
5. why each local extension exists
   - explain the responsibility gap it fills instead of leaving the reason implicit

Rules:

1. The seven-class local taxonomy is a standard-compatible local engineering taxonomy, not a literal copy of any single original standard directory.
2. If a project needs a more formal customer-facing or standard-facing package later, create a projection layer on top of the local formal doc root instead of deforming the local engineering taxonomy first.

### 2.3 Required second-level directories

Create or align:

1. `06_测试文档/01_自测报告/`
2. `06_测试文档/02_验收大纲/`
3. `06_测试文档/03_验收记录/`
4. `06_测试文档/04_验收结论/`
5. `06_测试文档/05_验收清单/`
6. `07_过程文档/01_会话交接/`
7. `07_过程文档/02_历史计划/`

Optional:

1. `03_规范与流程/01_数据规范/`
2. `03_规范与流程/02_关键流程/`
3. `03_规范与流程/03_设计实现映射/`
4. `03_规范与流程/04_原型与附图/`
5. `07_过程文档/03_验收意见处理/`

## 3. Tracker bootstrap

If the project has staged delivery, multiple contributors, or parallel tracks, create a tracker early.

Recommended tracker fields:

1. `Status`
2. `Phase`
3. `Contributes To`
4. `Work Type`
5. `Start Date`
6. `Target Date`

Before mutating remote tracker schema, decide:

1. whether GitHub Project, GitLab, or an equivalent remote board is the formal tracker layer for this project
2. whether the user allows remote-tool use for this project
3. whether the user allows schema changes such as new fields, status options, or views

If any of those answers is no or still unknown, keep detailed execution state in local execution contracts until approval is explicit.

Tracker responsibility:

1. schedule
2. roadmap
3. status
4. WBS visibility

Tracker should not hold:

1. long design derivation
2. full acceptance scripts
3. self-test logs
4. handoff detail

## 4. Execution contract bootstrap

Each executable task should follow this minimum structure:

```md
工作目标：
- ...

工作内容：
- ...

潜在难点：
- ...

Depends On：
- ...

成果物：
- ...

验收方法：
- ...

当前状态：
- ...

上级节点：
- ...
```

## 5. WBS bootstrap rules

1. Use WBS tree decomposition as the stable plan axis.
2. Name stable plan files by WBS node, not by temporary labels.
3. Use milestones such as `M1 / M2 / M3` as validation gates, not as the top-level decomposition axis.
4. Record the active node in the plan README and tracker.

## 6. Collaboration bootstrap rules

### 6.1 Dual-gate model

Separate:

1. `研发推进门`
2. `阶段关闭门`

Meaning:

1. development can continue on low-coupling preparation
2. phase close still requires explicit human acceptance

### 6.2 Prep / Core

Classify downstream work as:

1. `Prep`
   - low-coupling preparation
2. `Core`
   - formal implementation depending on stable upstream output

If upstream is still `待人工验收`:

1. `Prep` may continue
2. `Core` should not be treated as formally started

### 6.3 Status layering

Tracker may use coarse status.

Execution contracts should use finer states such as:

1. `待开发`
2. `开发中`
3. `已自测`
4. `待人工验收`
5. `已验收`
6. `阻塞中`

If remote schema changes are allowed, prefer:

1. a coarse `Status` field for schedule and roadmap readability
2. a separate `Execution Status` or `当前状态` field for the fine-grained execution states above

Only use a single six-state `Status` model when:

1. the user explicitly wants a single-field model
2. the tool cannot support two status-like fields cleanly
3. the existing board already depends on that model and migration cost is not justified

### 6.4 Shared path convention

In GitHub collaboration surfaces (Issue/Project/PR), use repository-relative paths by default.

Examples:

1. `DOC/CODEX_DOC/04_研制计划/01-WBS-0-<project>-研发总纲-研制计划.md`
2. `src/server/routes.js`

If collaborators need clickable links, add repository URLs:

1. `https://github.com/<owner>/<repo>/blob/<branch>/DOC/...`

Do not place workstation absolute paths such as `/home/...` in shared tracker artifacts.

## 7. Acceptance bootstrap

Minimum expectation after each real work round:

1. run meaningful validation
2. create or update self-test record
3. create or update acceptance checklist
4. create or update acceptance outline when the node baseline changes or is first introduced
5. create or update handoff record

Acceptance files should use timestamped naming.

Recommended patterns:

1. `YYYY-MM-DD-HHMMSS-主题自测.md`
2. `YYYY-MM-DD-HHMMSS-主题验收清单.md`
3. `YYYY-MM-DD-HHMMSS-主题验收记录.md`
4. `YYYY-MM-DD-HHMMSS-主题验收结论.md`

## 8. First-session bootstrap checklist

When adopting this template in a new project, perform this order:

1. inspect repo structure and current worktree
2. choose or create local doc root
3. create the seven-class numbered directory skeleton
4. write `README.md`
5. write `00-本地工程策略映射.md`
6. write `01_需求分析/00-工程总体分析.md`
7. write the initial `04_研制计划/` node docs
8. seed the initial `05_节点合同/` node contracts when the project uses local node contracts
9. create test and process subdirectories under `06_测试文档/` and `07_过程文档/`
10. create tracker if needed
11. link tracker and local docs together

## 9. Retrofit rule for existing projects

If the project already contains docs or task structures:

1. do not duplicate equivalent docs
2. normalize names and responsibilities gradually
3. flatten single-file topic directories when they add no classification value
4. archive obsolete detailed plans into `07_过程文档/02_历史计划/` instead of deleting history blindly
5. prefer alignment over large one-shot rewrites

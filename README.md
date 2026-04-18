# Project Engineering Strategy

Cross-session engineering workflow and acceptance governance for Codex.

This repository shape is intentionally split in two:

- repository root files are human-facing
- `project-engineering-strategy/` is the installable skill package

That keeps the published skill package clean while still giving the GitHub repo a clear landing page.

## What This Skill Helps Enforce

- read handoff, current plan, acceptance checklist, and recent self-test before editing
- stabilize models, contracts, runtime behavior, and event chains before UI polish
- keep tracker status, execution contracts, and local docs synchronized
- separate self-test evidence from human acceptance
- avoid treating isolated worktrees or temporary paths as official delivery paths

## Repository Layout

- `project-engineering-strategy/`
  - installable public skill package
- `README.md`
  - public landing page for humans

## Installation

Install the skill from this repository by targeting the `project-engineering-strategy/` path.

Example installer inputs:

- repo: `wgwtest/project-engineering-strategy`
- path: `project-engineering-strategy`

If you are using a GitHub URL-based installer flow, point it at the `project-engineering-strategy/` directory in this repo rather than the repository root.

## Why The Skill Is In A Subdirectory

The skill package intentionally does not live at repository root because the root also needs public-facing repo files such as this README. The subdirectory keeps the skill package spec-compliant and avoids mixing repo marketing files into the installable package.

## Versioning

- use Git tags for public release boundaries
- keep the skill package and this README aligned in the same release

## Maintainer Rule

If you are updating the public release from the source-of-truth repo, sync the public skill package into this repo before tagging or pushing.

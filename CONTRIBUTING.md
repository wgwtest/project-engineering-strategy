# Contributing

Thanks for improving this skill.

## What Helps Most

- sharper trigger wording in `SKILL.md`
- clearer examples that show when the skill should and should not be used
- tighter workflow guidance that reduces ambiguity
- public-safe references and examples that do not depend on private repos
- installation or packaging fixes that keep the public repo easy to use

## Contribution Rules

- Keep the installable package inside `project-engineering-strategy/`.
- Keep root files human-facing and package files skill-facing.
- Do not add local machine paths, private repo names, or project-specific residue.
- Prefer concrete prompts and real usage patterns over abstract theory.
- If you change workflow rules, update examples and root documentation in the same change.

## Pull Request Checklist

- explain the user problem or ambiguity being fixed
- keep the scope narrow
- update docs if behavior or packaging changed
- verify the public package still installs cleanly from the `project-engineering-strategy/` path

## Issues

Open an issue when reporting:

- install or upgrade problems
- trigger misfires
- unclear workflow rules
- contradictions between examples and the skill body
- ideas for high-value additions

# dotclaude

Personal Claude Code configuration, version-controlled straight from
`~/.claude`. The `.gitignore` is a whitelist: everything is ignored except
the paths it explicitly negates, because the rest of `~/.claude` is runtime
state (sessions, caches, credentials) that must never be committed.

## Contents

- `output-styles/adhd.md` — action-first, no-preamble output style. Adapted
  from [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) (MIT):
  converted from a skill to a Claude Code output style, time-estimate rule
  dropped, list-cap rule replaced with rank-don't-cap, harness carve-outs
  added for agentic use (tool-call announcements, lead-with-outcome reports,
  handoff-only-when-it's-yours).

## Install

This repo is a Claude Code plugin marketplace. Native install:

```bash
claude plugin marketplace add cbini/dotclaude
claude plugin install dotclaude@dotclaude
```

The `adhd` style then appears in the `/config` output-style picker
(unprefixed — plugin output styles are not namespaced). Claude Code keeps
marketplace-installed plugins updated.

Manual alternative: copy `output-styles/adhd.md` into
`~/.claude/output-styles/` (all projects) or `.claude/output-styles/`
(one project). Don't do both — two sources of the same style name.

## Use

Select `adhd` under `/config` → Output style, or set it directly:

```json
{ "outputStyle": "adhd" }
```

in `.claude/settings.local.json` (per-project) or `~/.claude/settings.json`
(global). The `/output-style` command was removed in Claude Code v2.1.91;
`/config` is the replacement.

## Adding config to version control

Negate the path in `.gitignore`, then `git add` it. Keep the whitelist
tight — when in doubt, leave it ignored.

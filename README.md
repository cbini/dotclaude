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

## Use

Activate per-project by adding to `.claude/settings.local.json`:

```json
{ "outputStyle": "adhd" }
```

or globally in `~/.claude/settings.json`. Where the `/output-style` command
is available, `/output-style adhd` does the same thing.

## Adding config to version control

Negate the path in `.gitignore`, then `git add` it. Keep the whitelist
tight — when in doubt, leave it ignored.

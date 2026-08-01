# dotclaude

Personal Claude Code configuration, version-controlled straight from
`~/.claude`. The `.gitignore` is a whitelist: everything is ignored except
the paths it explicitly negates, because the rest of `~/.claude` is runtime
state (sessions, caches, credentials) that must never be committed.

## Contents

- `output-styles/adhd.md` — action-first, no-preamble, plain-language output
  style. Adapted from
  [ayghri/i-have-adhd](https://github.com/ayghri/i-have-adhd) (MIT):
  converted from a skill to a Claude Code output style, time-estimate rule
  dropped, list-cap rule replaced with rank-don't-cap, harness carve-outs
  added for agentic use (tool-call announcements, lead-with-outcome reports,
  handoff-only-when-it's-yours), plus a plain-language section covering word
  choice, sentence length, active voice, self-contained references, and
  summary-before-detail.

### Readability sources

The plain-language rules (10 to 14) narrow these standards to what applies to
a technical reader in a terminal:

- [ISO 24495-1:2023](https://www.iso.org/standard/78907.html) — plain
  language, governing principles
- [WCAG 2.1 SC 3.1.5 Reading
  Level](https://www.w3.org/WAI/WCAG21/Understanding/reading-level.html),
  with techniques [G153](https://www.w3.org/WAI/WCAG21/Techniques/general/G153)
  (making text easier to read) and
  [G86](https://www.w3.org/WAI/WCAG21/Techniques/general/G86) (plain-language
  summary of complex text)
- [Inclusion Europe, *Information for
  all*](https://www.inclusion-europe.eu/wp-content/uploads/2017/06/EN_Information_for_all.pdf)
  — European easy-to-read standards
- [digital.gov plain language guide](https://digital.gov/guides/plain-language)
- [Harvard: designing for
  readability](https://accessibility.huit.harvard.edu/design-readability)

Rules that govern visual presentation (font size, line spacing, contrast,
column width) are out of scope — Claude Code does not control the terminal's
rendering.

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

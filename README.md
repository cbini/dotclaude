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
  take-your-own-next-step, handoff only when it's genuinely the reader's),
  plus a plain-language section covering word choice, consistent naming,
  sentence length, active voice, imperatives, self-contained references, and
  summary-before-detail.

### Readability sources

The sentence rules (S1 to S22) narrow these standards to what applies to
a technical reader in a terminal. The sources are listed here rather than in
the style file — the style file holds only text that changes the output:

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
- [Plain English Campaign, *How to write in plain
  English*](https://cdn.website-editor.net/s/08adc49f98924cb8b7dddec4cafb071e/files/uploaded/howto.pdf)
  — source of the 15-to-20-word sentence average and the words-to-avoid list
- [Harvard: designing for
  readability](https://accessibility.huit.harvard.edu/design-readability)
- [ASD-STE100 Simplified Technical English](https://asd-ste100.org/), Issue 9,
  by way of [AminBlg/SimpleEnglish](https://github.com/AminBlg/SimpleEnglish)
  — source of S8 (three-word name limit), S14 (simple tenses), S15 (no
  trailing "-ing" clause), S17 (keep articles, "that", and full negatives),
  S18 (condition before command), the 20-word ceiling on steps, the
  one-kind-of-item list rule, and the paragraph bounds in O1. Its ban on
  `should`/`may`/`might` is deliberately not adopted: R8 requires a hedge
  when the uncertainty is real. Its ban on all phrasal verbs is not adopted
  either, because "set up" is the common word and S1 asks for the common
  word. Its approved-word dictionary does not transfer — the style has no
  word list to check against.

Rules that govern visual presentation (font size, line spacing, contrast,
column width) are out of scope — Claude Code does not control the terminal's
rendering.

## Install

This repo is a Claude Code plugin marketplace. Native install:

```bash
claude plugin marketplace add cbini/dotclaude
claude plugin install dotclaude@dotclaude
```

The style then appears in the `/config` output-style picker as **ADHD**
(the `name` in the file's frontmatter, not the filename). Claude Code keeps
marketplace-installed plugins updated. Note that the settings value is
namespaced — `dotclaude:ADHD`, not `ADHD` — see [Use](#use).

Manual alternative: copy `output-styles/adhd.md` into
`~/.claude/output-styles/` (all projects) or `.claude/output-styles/`
(one project). Don't do both — two sources of the same style name.

## Use

Select the style under `/config` → Output style, or set it directly in
`.claude/settings.local.json` (per-project) or `~/.claude/settings.json`
(global). The value depends on how you installed it. After the plugin
install above:

```json
{ "outputStyle": "dotclaude:ADHD" }
```

Plugin-provided styles are namespaced `plugin-name:style-name`, so the bare
frontmatter name does not resolve. After the manual copy into an
`output-styles/` directory, use the bare name instead:

```json
{ "outputStyle": "ADHD" }
```

An unresolvable value fails silently — Claude Code falls back to the default
style and logs no error, so a typo looks exactly like the style not loading.

The `/output-style` command was deprecated in Claude Code v2.1.73 and removed
in v2.1.91; `/config` is the replacement. In the VS Code extension (checked on
v2.1.220) `/config` takes `key=value` arguments with no interactive picker, and
its `outputStyle` values are the built-in styles only — set a plugin style in
settings there.

Two things to expect:

- The style is part of the system prompt, which Claude Code reads once at
  session start. A change takes effect after `/clear` or in a new session —
  editing the file mid-session does nothing until then.
- It applies to the main conversation only. Subagents run their own system
  prompt, so they answer in the default style. A fork is the exception, since
  it inherits the parent's full system prompt.

`keep-coding-instructions: true` in the frontmatter is deliberate: this style
changes how Claude communicates, not how it codes, so Claude Code's built-in
software-engineering instructions stay in place. Dropping that field would
remove them.

## Adding config to version control

Negate the path in `.gitignore`, then `git add` it. Keep the whitelist
tight — when in doubt, leave it ignored.

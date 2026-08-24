# A/B verification plan: adhd.md vs adhd-v2.md

Do not claim v2 improved compliance until this test says so. The predictions
and the outcomes that would falsify them are at the end.

## Arms

- **A**: `output-styles/adhd.md` (original, 3,418 words)
- **B**: `output-styles/adhd-v2.md` (revision, 2,911 words)
- **C** (reference ceiling): `.github/PLAIN_LANGUAGE.md` from
  `TEAMSchools/teamster` — the 42-line derivative that won the first test

## Protocol

- N = 10 runs per arm per task. The first test was n = 1 per arm; sampling
  variance alone can produce its result, so nothing under ~10 runs settles a
  comparison.
- Same model for every cell (the first test used Sonnet; any fixed model
  works, but never mix models across arms).
- One isolated subagent per run. Its only tool use is a single Read of its
  arm's style file; the rest of the prompt is identical across arms.
- Scoring: grep for the mechanical metrics; hand-judge the rest with the
  arm labels hidden (shuffle the outputs first — knowing the arm biases the
  judge).

## Task 1 — PR body (document surface)

Prompt, verbatim except `{STYLE_FILE}`:

> Read the file `{STYLE_FILE}` in full. It is your writing style guide: it
> governs everything you write in this task, as if it were part of your
> system prompt. Apply it silently — never mention or quote it.
>
> Then write a GitHub pull request body from the change brief below, using
> the PR template below. Use no other tools. Your final message must be ONLY
> the finished PR body markdown — no commentary before or after it.
>
> === PR TEMPLATE ===
>
> # Pull Request
>
> > **Write this whole PR in plain language.** Follow the writing style
> > guide you were given: every sentence does a job, one idea per sentence,
> > active voice, common words.
>
> ## Summary & Motivation
>
> > What changed and why. A reviewer skimming just this section should
> > understand the change. Save tradeoffs, edge cases, and verification
> > detail for "Reviewer Notes" below.
>
> "When merged, this pull request will..."
>
> ## Reviewer Notes
>
> > Optional. Name what's worth a second look and why, in a line or two
> > each. Delete if there's nothing here.
>
> ## Self-review
>
> > Complete only the sections relevant to your changes.
>
> - [ ] Tests updated for the new behavior
> - [ ] Config change documented in the deploy runbook
> - [ ] Rollback plan stated in the summary above
>
> === CHANGE BRIEF (raw notes from the change author) ===
>
> - added TTL based eviction to the report cache. entries now expire 6h
>   after write instead of living until the nightly restart clears them
> - config: `cache.ttl_hours` in `config/settings.yaml`, default 6
> - the export endpoint reads the same cache, so exports also pick up the
>   6h bound
> - measured in staging: p95 for /reports went from 840ms to 210ms after
>   warm-up. did not measure prod. prod has ~10x traffic so prod numbers
>   are a guess for now
> - reviewer needs to: run migration `2024_add_cache_meta.sql`, set
>   `cache.ttl_hours` in the prod overrides, deploy worker before web
> - SLA context: support promised customers report data no staler than 8
>   hours. this change is what actually enforces that promise
> - known gap: eviction sweep runs every 15 min, so worst case staleness
>   is 6h15m

The brief plants one trap per targeted rule: 2 acronyms the reader never
used (TTL, SLA), a verified staging number next to a guessed prod number,
ordered reviewer steps sitting beside 2 plain facts that tempt one mixed
list, and a template line the first test saw deleted. `p95` is a metric
identifier, not an acronym — do not count it.

### Task 1 metrics (per run)

1. TTL expanded at first use — "time to live (TTL)" or equivalent before
   any bare use (y/n). Same for SLA ("service level agreement").
2. The prod-performance claim marked as inferred, unverified, or a guess,
   distinctly from the measured staging number (y/n).
3. Mixed list: any plain-fact item inside a checkbox or step list (y/n —
   a violation).
4. The line "When merged, this pull request will..." present and completed
   (y/n).
5. Supplied template sections missing (count; 0 is a pass).
6. Banned opener, recap, or closer phrases (count).
7. Words of governed prose (Summary & Motivation + Reviewer Notes) — a
   check that arms write comparable amounts, not a target.
8. New-artifact screen: narrated compliance ("to keep this brief",
   "checking acronyms"), quoted rule numbers, or a style mention (count).

## Task 2 — chat turn (conversation surface)

Same wrapper prompt, swapping the template and brief for:

> You just did the following for a user, in this order: ran their test
> suite (3 passed, 1 failed — `auth.spec.ts:42` expected 200, got 401);
> found the request was missing an auth header; added the header in
> `tests/auth.spec.ts`; reran the suite (all 4 pass). One thing remains
> that only the user can do: set `AUTH_SECRET` in their production
> environment before deploying. Write your reply to the user.

### Task 2 metrics (per run)

1. First line states the outcome or an action — not context, not "I
   looked into..." (y/n).
2. Exactly one handoff, at the end, naming `AUTH_SECRET` as the user's own
   step (y/n).
3. Banned openers/closers (count).
4. State restated — the pass/fail counts appear (y/n).

## Predictions

- B beats A on Task 1 metrics 1–4, the targeted failures. C lands near B on
  metrics 1–3; C has no template rule, so metric 4 may tie A.
- B ties A on metric 7 — the first test tied at 238 words, and nothing in
  the revision predicts shorter output, only more compliant output.
- B ties A on every Task 2 metric. The reorder moved the turn rules deeper
  into the file; the claim is that their section, examples, and the closer
  hold them.

## Falsification — results that mean the revision failed

1. B ≤ A on acronym expansion or on mixed lists across N = 10: the
   example-coverage bet (H2) is wrong or insufficient. Next lever: cut
   depth toward C's 42-line density, not more structure.
2. **B < A on Task 2's lead-with-action or single-handoff metrics: the
   revision made compliance worse** — the reorder traded the surface that
   worked for the surface that failed. Restore the response section to
   first position and rerun.
3. B deletes template lines A kept, or Task 1 metric 8 fires (narrated
   compliance, quoted rule numbers): the new blocks — the precedence
   block, R6 — backfired. Also worse.
4. B beats A only where outputs echo the file's own example vocabulary
   ("inferred, not checked") and paraphrase cases still fail: the file
   taught strings, not rules. Rerun with a second brief (different
   acronyms, a differently-phrased hedge) before believing any of it.

## Pilot run, 2026-08-24 (n = 4 per arm, arms A and B, Task 1 only)

Run in this session to prove the metrics are countable, using the exact
prompt above with Sonnet subagents. n = 4 settles nothing — treat it as a
harness check with a directional reading, and note the scorer was the
revision's author, unblinded.

| Metric, per run                        | A: adhd.md          | B: adhd-v2.md |
| -------------------------------------- | ------------------- | ------------- |
| runs with an unexpanded bare acronym   | 2 of 4 (TTL, SLA)   | 0 of 4        |
| prod claim marked inferred or a guess  | 4 of 4              | 4 of 4        |
| mixed-list violations                  | 0 of 4              | 1 of 4        |
| "When merged..." line kept + completed | 4 of 4              | 4 of 4        |
| template sections missing              | 0                   | 0             |
| banned phrases / narrated compliance   | 0                   | 0             |
| governed words (Summary + Notes)       | 160–176, mean 164   | 166–187, mean 177 |

5 readings, held to what n = 4 supports:

1. The acronym direction matches the prediction — B never missed, A missed
   in 2 of 4 runs (a TTL gloss with no expansion; a bare "8-hour SLA") —
   and matches the first test's failure. Directional signal only.
2. Two of the first test's 3 failures did not reproduce in arm A at n = 4:
   inference marking and the template line went 4 of 4. The n = 1 test
   overstated how broken the original is on those metrics. Rates, not
   existence, are the thing to measure — hence N = 10.
3. Against the revision: the pilot's only mixed-list violation came from
   arm B (run 1 put an action item — "Add one before merging." — inside a
   fact bullet list). One run proves nothing, but the direction is the
   wrong way, and falsification line 1 watches exactly this metric.
4. Taught-strings watch (falsification line 4): all 4 B runs hedge prod in
   the file's own example vocabulary ("inferred, not measured"); A runs
   vary ("a guess," "an estimate"). The reader is served either way, but
   run the second brief before crediting the rule over the string.
5. Both arms usually handled SLA by avoiding the acronym ("the 8-hour
   promise") — a pass under the metric as defined, since the violation is
   bare use without expansion. B also wrote no shorter output than A
   (+13 words mean): the revision predicts compliance, not compression,
   and the pilot agrees so far.

Raw outputs: `docs/pilot/{a1..a4,b1..b4}.md` — governed prose only, with
the template scaffolding stripped for the word counts.

Staleness note: the pilot ran against a v2 draft whose closer ended with a
3-item self-check naming these exact metrics. That check was cut right
after the pilot, so runs b1–b4 saw a file the current v2 no longer is.
The check named the acronym metric, the one B swept — rerun against the
current file before crediting B's 0 of 4 to the rules alone.

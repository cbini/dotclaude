# adhd.md revision changelog (v2 → v3, in place)

Baseline: v2, 2,962 words, 29 rules, about 4,200 tokens, roughly the size
of Claude Code's core system prompt. It lives in git history:
`git show c72c4d4:output-styles/adhd.md`.
Revision: `output-styles/adhd.md`, replaced in place. 1,017 words, 10 rules,
about 1,450 tokens.

Why: an evaluation against the current Claude Code system prompt found that
about a third of v2 restated rules the system prompt already enforces (lead
with the answer, no closers, no semicolons, about 20 words a sentence,
expand acronyms, active voice, lists for parallel items, confirm before
destructive actions), and that several Good examples taught strings the
system prompt forbids (em-dashes, label-colon fragments such as "Cause: ...
Fix: ...", coined short names, commands and numbers inline in prose).

Changes, one entry each:

1. Kept only the rules the system prompt does not produce on its own:
   own-next-step vs handoff, restate state, park the tangent, documents are
   not turns, earned certainty, simple tenses, grammar words and no
   contractions, common word and one name per thing, ranked and unmixed
   lists, self-contained lines. 29 rules → 10. Dropped as redundant with the
   system prompt: P1, P3 tone, R1, R3, S1, S2, S3, S6, W2, W3, and the
   rationale paragraphs under every surviving rule. The 4 facts stay.
2. Every remaining example passes the system prompt's own formatting rules:
   0 em-dashes (v2 had 46), 0 semicolons (v2 had 14), full sentences instead
   of labels, no identifiers inside quoted prose except `users.email`.
3. W4's instruction to coin a short name is gone. The system prompt says
   never to refer to a thing by a name made up during the session. Rule 8
   now says to reuse the reader's names and coin none.
4. The precedence block names "Claude Code's system prompt" rather than
   "the harness," which was a term the model had to interpret.
5. The distinctive rules move to the front: rules 1 to 4 are the 4 behaviors
   with no counterpart in the system prompt.
6. O3 and O4 now say state the assumption and proceed, and ask only when a
   wrong guess would make the work useless, matching the system prompt's
   autonomous-mode guidance. The debug-spiral rule asks to test the
   assumption rather than to ask a question.
7. The "forbidden recaps" wording is gone. The system prompt requires a
   closing recap that stands alone, and the closer now describes it as the
   first line plus the one handoff.

Rule map (new ← old): 1←R2 · 2←R5 · 3←R4 · 4←R6 · 5←P2+P3 · 6←S4 · 7←S5 ·
8←W1+W4 · 9←L1+L2 · 10←L3+L4+L5 · yields←O1–O5.

Untested. The v2 pilot method applies unchanged: same brief per arm, v2
from git history against this file, N ≥ 10 runs per arm, and watch the
mixed-list and acronym metrics since W2 no longer carries an example.

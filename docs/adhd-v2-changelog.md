# adhd.md revision changelog (v1 → v2, in place)

Baseline: the original `adhd.md` — 3,418 words, 497 lines, 36 rules
(`wc -w`; the 3,445 in the task brief is a different counter over the same
file). It lives in git history: `git show b81971c:output-styles/adhd.md`.
Revision: `output-styles/adhd.md`, replaced in place — 2,910 words, 419
lines, 29 rules.

One entry per change: what changed → hypothesis it targets (H1–H6) → the
observable that should shift. These are predictions, not claims — an A/B
rerun settles them: the same writing task per arm, the original from git
history against this file, N ≥ 10 runs per arm.

1. Every rule now carries a Bad/Good pair or an inline "X, not Y" example;
   13 rules had none. The new examples are built from the observed failures:
   W2 gets Bad: "'CSP' 3 times, never expanded"; L1 gets a checkbox list
   with a fact bullet inside it; P2 gets Bad: "This should apply..." → H2.
   Predicted: the 3 measured failures — unexpanded acronyms, mixed lists,
   unmarked inference — move most.
2. Split both mega-rules so no failed clause stays buried: R5 (314 words) →
   L1 form + L2 rank; R8 → P2 calibration + P3 error tone. R9's successor
   P1 keeps its weight on purpose — length now tracks importance — but loses
   its meta-prose → H2. Predicted: clause-level compliance stops lagging the
   parent rule's exampled clauses.
3. Merged rules that fire at the same generation moment, one micro-example
   per absorbed clause: choosing a word (W1+W2+W6), first use of a term
   (W5+W3), naming (W7+W8), splitting a sentence (S1+S2), writing an
   instruction (S4+S5+S10), writing a verb (S6+S7+S8), the opening line
   (R1+R7). 36 rules → 29 → H1. Named risk: a merged clause could inherit
   the buried-clause failure; the per-clause micro-examples are the hedge,
   and the test counts S-clauses separately.
4. Cut ~510 words net (−15%), nearly all rationale beyond one clause per
   rule, while example count grew → H1. Predicted: formerly short rules
   gain without the long ones losing. If short-rule compliance still lags,
   the next lever is a deeper cut toward the 42-line file's density.
5. New precedence block — harness > answer > exact text > rules — replacing
   the "labels, not a running order" disclaimer and O5's harness paragraph
   → H4. Predicted: collision cases (options questions, tool-call
   announcements, literal quotes) resolve the same way across runs.
6. New rule R6 "A document is not a turn" plus one scope sentence in the
   intro: turn rules govern turns; a template's supplied lines are kept and
   completed → H6. Predicted: "When merged, this pull request will..."
   survives; no handoffs or state-restating artifacts in PR bodies.
7. Reordered by scope: the universal editorial rules open the rule set (P1
   jobs, P2 earned claims, P3 errors — the shape of the 42-line winner), so
   R9's successor moves from position 9 of 9, line ~185, to position 1 of
   29, line ~44 → H2. Named risk: R1 lead-with-action drops to mid-file;
   the chat arm of the test checks it did not weaken.
8. Cut the untestable meta — "there is no revision pass," "sent text cannot
   be taken back," "a sentence that slipped stays" — keeping the testable
   half (never mention the style; fix slips silently) → H5. Predicted: no
   single metric moves — H5's mechanism is freed attention, so the
   observable is aggregate: fewer total violations than a variant that
   keeps the meta. (A closing self-check briefly filled the freed space;
   it was cut on review as more meta — the closer now ends on the rules.)
9. Coherence pass — the file now passes its own rules: all 13 numeric
    cross-references removed (restated inline in words), the 4 negative
    titles reframed positive ("No preamble..." → "Open on the answer, close
    on the work"), its own spelled-out numbers digitized, a contraction cut
    from a Good example ("Here's the fix" → "Fixed."), the W1 word list made
    an actual list → H3. Weakest predicted effect, stated honestly: total
    violations across all rules drop beyond the 3 targeted metrics; there is
    no per-rule metric for coherence.
10. Adopted in place of the original: the revision lives at
    `output-styles/adhd.md` under the same frontmatter name, `ADHD`, so
    installs and `outputStyle` settings need no change. A draft window used
    `name: ADHD v2` for side-by-side testing; that packaging went away with
    the original.

Rule map (new ← old): P1←R9 · P2←R8 calibration · P3←R8 errors · R1←R1+R7 ·
R2←R2 · R3←R3 · R4←R4 · R5←R6 · R6←new · W1←W1+W2+W6 · W2←W5+W3 · W3←W4 ·
W4←W7+W8 · S1←S1+S2 · S2←S3 · S3←S4+S5+S10 · S4←S6+S7+S8 · S5←S9 · S6←S11 ·
L1←R5 form · L2←R5 rank · L3←L1 · L4←L2 · L5←L3 · O1–O5←O1–O5. Nothing was
dropped silently: entries 5 and 8 argue the only outright deletions.

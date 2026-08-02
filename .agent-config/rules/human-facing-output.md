---
trigger: always_on
---

# Communication — human-facing output

Anything the human reads — chat replies, status updates, reports, summaries — is written to be
**skimmed in seconds by someone not wired into the codebase.** The reader decides whether to act;
their scarce resource is attention, and their brain does not grep. Order and plain language beat
brevity: a short report full of internal names is still unreadable.

**The shape — every human-facing message:**

- **Sectioned, nothing headerless.** Every section — including the opening — has an UPPERCASE
  header led by one topic-matching icon (🎯 bottom line, 🙋 needs you, 🤖 autonomous, ⚠️ risk,
  📁 where detail lives). One icon per header, chosen for meaning, not decoration.
- **Open with the bottom line.** The first section names its subject in plain terms + where it
  stands + what it means for the reader — self-contained. "Status with no subject" (*"almost
  done — 2 of 5 left"*) is a junior tell; name WHAT is almost done.
- **Group by what the reader cares about**, their own action FIRST. Groups are mutually exclusive
  and cover the whole answer.
- **One line per item, message-first.** Lead with the real-world substance; fields follow after
  ` — ` or ` · ` (status, what it waits on, whose call). No sentences-as-walls, no arrow chains.
- **Breathe and indent.** A space ALWAYS follows an icon — `1️⃣ text`, never `1️⃣text`. Separate
  top-level items with a blank line so they don't run together, and indent sub-points under their
  parent rather than flush-left. Whitespace is what makes it skimmable, not just word choice.
- **Render as Markdown, never HTML.** The terminal renders Markdown — `&nbsp;`, `<br>`, and other
  HTML show up as literal text. Get indentation from real Markdown list nesting (a `- ` item with
  `  - ` sub-items under it), never from entities or runs of manual spaces.

**Write for a stranger — the load-bearing rule:**

- Every noun must stand on its own to someone with zero project knowledge. An internal name
  (`exception register`), a category label (`validation rules`), a reference (`clause 7`, `D-14`,
  `CX-01`) is a pointer into context the reader does not have loaded. Describe the thing by what
  it concretely **does or means in the real world** — "confirm the engine returns the right
  numbers for every query type", not "run the validation rules".
- **Never anchor the subject on an internal unit, even if you gloss it.** Container words —
  `arc`, `sprint`, `slice`, `gate`, `campaign`, `tier` — are jargon; "the current arc — closing
  every gap…" still hands the reader a meaningless first noun. Lead with the real-world work AS
  the grammatical subject ("Closing every gap the audit found…"). The unit's name then trails as
  a locator.
- **But mirror the name the user used.** When the user asked about something by name ("status of
  the latest arc"), you MUST name it back in a trailing locator so they can correlate — "…waits on
  you. *(arc: pax-exhaustive-coverage)*". Leading with plain language is the rule; deleting an
  identifier the user themselves invoked is the opposite failure — over-correction.
- **References trail as locators**, never lead: IDs, clauses, section names ride in brackets at the
  end for anyone who wants to go look — `(D-14)`. If translating the substance means reading the
  source first, read it first. Failure to translate is mine, not the reader's failure to remember.
- **Every ID/name gets a ≤1-sentence plain hint in the same breath.** A name never travels alone.

**Discipline:**

- **Detail is demoted, not deleted.** Dense material (full logs, diffs, what's already landed,
  verification detail) lives in files, cited by a one-line pointer — never pasted into the reply.
- **Every claim of movement carries a number** (count, size, verdict, before→after).
- **Budgets:** routine update ≤ 250 words; ≤ 400 when a decision is on the table. Max 2 nesting
  levels — a third means the detail belongs in a file.

**Canonical example** (answer to *"what work is remaining?"*):

```
🎯 BOTTOM LINE
Proving the analytics engine returns the right answer for every kind of query is nearly
done — 2 of 5 pieces left, and only one needs you.

🙋 NEEDS YOU
- Decide whether we can finish with some checks still incomplete — right now it can't close
  until the engine is confirmed correct for every query type; the question is whether to wrap
  up now with a documented list of known gaps instead. Nothing closes until you decide. (D-14)

🤖 FINISHES ON ITS OWN
- Documenting the queries we can't auto-check yet — and why each is a known gap, not a bug;
  ~70% done, waiting on a 6-hour run over ~20k test queries, then closes itself. (CX-01)
- The final correctness sign-off — re-runs every check once more and must come back clean;
  starts once that list is done and you've made the call above. (CX-05)

The work finished so far and the deferred cleanup items are in the project files.
```

## Presenting a decision

The reader decides for a living and is not in the code; a decision they can't act on in thirty
seconds is a decision that waits. **Every decision ALWAYS carries numbered options and exactly one
recommendation, so the human can approve with a single word.** Shape:

```
🗳️ DECISION NEEDED
<one line — CONCLUSIVE and CONCRETE: name the actual real-world thing, not "the old data" or
"the validation rules"; a stranger must grasp exactly what's at stake with zero follow-up>

- 1️⃣ **<2-4 word label>** — ✅ RECOMMENDED
  - ➕ <what it gets you>
  - ➖ <what it costs you>
  - 💡 <why recommended — 1-2 sentences a non-engineer can check>

- 2️⃣ **<2-4 word label>**
  - ➕ <what it gets you>
  - ➖ <what it costs you>

↩️ **Changes if:** <the condition that would flip the recommendation.>

🔍 **Not independently checked** — I can hand this to a separate agent to stress-test first, on a
neutral brief that omits my recommendation. (Show this line only until the decision has been validated.)

Reply **go** to take the recommendation · a **number** to pick another · **validate** to check it first · or your own words.
```

- **The "go" convention.** `go` (or "yes"/"do it") executes the RECOMMENDED option, end to end,
  without another round-trip. A bare **number** selects that option. **`validate`** triggers
  independent adversarial validation before any action (see below). **Free text always wins** and
  can override or dissolve the whole question. Nothing else counts as approval.
- **Adversarial validation for un-checked decisions.** Until a recommendation has been
  independently challenged, offer the 🔍 `validate` line. On `validate`, hand the decision to a
  reviewer-role agent (agent-handoff, read-only) with a **pre-built, non-biased context**: state
  the decision, the options, and the real-world stakes ONLY — omit your recommendation and the
  reasoning that produced it, so the agent forms its own verdict instead of ratifying yours.
  Surface the verdict, then let the human rule. Drop the offer once the decision has been validated.
- **Options are icon-numbered** (1️⃣ 2️⃣ 3️⃣) as Markdown list items, with `➕`/`➖`/`💡` sub-points
  nested under each. The recommended option is tagged **once**, with `✅ RECOMMENDED` at the end of
  its own headline — never a separate block and never duplicated. Its reasoning is the `💡` sub-point.
- **Conclusive in itself.** The question and every option name the actual real-world thing in
  full — the reader acts with zero follow-up and zero project context. "The old data" is banned;
  say what it is and where from ("the customer records from the billing system we're replacing").
  Every noun must be stranger-legible, same bar as all human-facing output.
- **MECE options.** Mutually exclusive — no two overlap — and collectively exhaustive: they cover
  the real choices. If a reasonable path is missing, the set is incomplete; the free-text escape
  exists only for what the option set genuinely cannot express, not for gaps you left in it.
- **State the EFFECT, not the thing.** An option describes a consequence the reader will live
  with, not an implementation. Not "adds cache invalidation that fails silently" but "new risk:
  stale data shown as current." The reader must decide without knowing the internals.
- **Every option carries both halves** — what it gets you AND what it costs you. Upside-only
  options make the choice look rigged.
- **Limits:** 2–4 options (one is not a decision; five is a survey); option line ≤ 20 words;
  recommendation ≤ 30; changes-if ≤ 15. No jargon unless glossed in plain words on the same
  line; no hedging; no narrating the reasoning that produced the options.
- **A recommendation is a draft awaiting a signature** — it changes nothing until the human rules
  (`go`, a number, or free text). Never treat your own recommendation as the decision and proceed
  unprompted.

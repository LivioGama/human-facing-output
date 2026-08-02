# Human-Facing Output

![Status](https://img.shields.io/badge/status-always%20on-1f883d)
![Type](https://img.shields.io/badge/type-global%20rule-black)
![Scope](https://img.shields.io/badge/scope-all%20agents-blue)
![Audience](https://img.shields.io/badge/audience-humans-6f42c1)

<a href="https://liviogama.github.io/agent-config/redirect.html?url=https://raw.githubusercontent.com/LivioGama/human-facing-output/main/.agent-config/rules/human-facing-output.md"><img src="https://raw.githubusercontent.com/LivioGama/agent-config/main/assets/install-badge-small.jpg" alt="Install human-facing-output global rule" height="40" /></a>

### Skimmed in seconds by someone not wired into the codebase

`human-facing-output` is an always-on global rule that reshapes everything an agent shows a human — chat replies, status updates, reports, summaries, decisions — into a form a stranger can act on without follow-up. The reader's scarce resource is attention; their brain does not grep. Order and plain language beat brevity.

No mode, command, or user intervention is required. Every human-facing message is automatically sectioned, bottom-lined, and written for a reader with zero project context.

## 🎯 What It Is For

A reply can be short and still be unreadable — full of internal names, status with no subject, options that hide the effect, or a recommendation the agent treats as already decided. The reader decides whether to act, in seconds, while looking at something else.

This rule makes agents automatically:

- open with the bottom line — the real-world subject, where it stands, what it means;
- section every message under an UPPERCASE, icon-led header;
- group items by what the reader cares about, their own action first;
- write for a stranger — every noun stands on its own, references trail as locators;
- demote dense detail to files, cited by a one-line pointer;
- put a number on every claim of movement;
- present every decision as numbered options with exactly one recommendation, approvable with a single word.

## 📐 The Rule

> Anything the human reads is written to be skimmed in seconds by someone not wired into the codebase. Order and plain language beat brevity. The reader decides whether to act; their brain does not grep.

Every human-facing message is sectioned, bottom-lined, and stranger-legible. Every decision carries numbered options and exactly one recommendation. A recommendation is a draft awaiting a signature — it changes nothing until the human rules.

## 🧱 The Shape — Every Human-Facing Message

- **Sectioned, nothing headerless.** Every section — including the opening — has an UPPERCASE header led by one topic-matching icon (🎯 bottom line, 🙋 needs you, 🤖 autonomous, ⚠️ risk, 📁 where detail lives). One icon per header, chosen for meaning, not decoration.
- **Open with the bottom line.** The first section names its subject in plain terms + where it stands + what it means for the reader — self-contained. "Status with no subject" (*"almost done — 2 of 5 left"*) is a junior tell; name WHAT is almost done.
- **Group by what the reader cares about**, their own action FIRST. Groups are mutually exclusive and cover the whole answer.
- **One line per item, message-first.** Lead with the real-world substance; fields follow after ` — ` or ` · ` (status, what it waits on, whose call). No sentences-as-walls, no arrow chains.
- **Breathe and indent.** A space ALWAYS follows an icon — `1️⃣ text`, never `1️⃣text`. Separate top-level items with a blank line; indent sub-points under their parent. Whitespace is what makes it skimmable, not just word choice.
- **Render as Markdown, never HTML.** The terminal renders Markdown — `&nbsp;`, `<br>`, and other HTML show up as literal text. Get indentation from real Markdown list nesting, never from entities or runs of manual spaces.

## 🧭 Write for a Stranger — the Load-Bearing Rule

- Every noun must stand on its own to someone with zero project knowledge. An internal name (`exception register`), a category label (`validation rules`), a reference (`clause 7`, `D-14`, `CX-01`) is a pointer into context the reader does not have loaded. Describe the thing by what it concretely **does or means in the real world** — "confirm the engine returns the right numbers for every query type", not "run the validation rules".
- **Never anchor the subject on an internal unit, even if you gloss it.** Container words — `arc`, `sprint`, `slice`, `gate`, `campaign`, `tier` — are jargon; "the current arc — closing every gap…" still hands the reader a meaningless first noun. Lead with the real-world work AS the grammatical subject. The unit's name then trails as a locator.
- **But mirror the name the user used.** When the user asked about something by name ("status of the latest arc"), name it back in a trailing locator so they can correlate — "…waits on you. *(arc: pax-exhaustive-coverage)*". Leading with plain language is the rule; deleting an identifier the user themselves invoked is the opposite failure — over-correction.
- **References trail as locators, never lead:** IDs, clauses, section names ride in brackets at the end for anyone who wants to go look — `(D-14)`. If translating the substance means reading the source first, read it first.
- **Every ID/name gets a ≤1-sentence plain hint in the same breath.** A name never travels alone.

## 📏 Discipline

- **Detail is demoted, not deleted.** Dense material (full logs, diffs, what's already landed, verification detail) lives in files, cited by a one-line pointer — never pasted into the reply.
- **Every claim of movement carries a number** (count, size, verdict, before→after).
- **Budgets:** routine update ≤ 250 words; ≤ 400 when a decision is on the table. Max 2 nesting levels — a third means the detail belongs in a file.

## 🗳️ Presenting a Decision

The reader decides for a living and is not in the code; a decision they can't act on in thirty seconds is a decision that waits. **Every decision ALWAYS carries numbered options and exactly one recommendation, so the human can approve with a single word.**

```
🗳️ DECISION NEEDED
<one line — CONCLUSIVE and CONCRETE: name the actual real-world thing; a stranger must grasp
exactly what's at stake with zero follow-up>

- 1️⃣ **<2-4 word label>** — ✅ RECOMMENDED
  - ➕ <what it gets you>
  - ➖ <what it costs you>
  - 💡 <why recommended — 1-2 sentences a non-engineer can check>

- 2️⃣ **<2-4 word label>**
  - ➕ <what it gets you>
  - ➖ <what it costs you>

↩️ **Changes if:** <the condition that would flip the recommendation.>

🔍 **Not independently checked** — I can hand this to a separate agent to stress-test first, on a
neutral brief that omits my recommendation. (Shown only until the decision has been validated.)

Reply **go** to take the recommendation · a **number** to pick another · **validate** to check it first · or your own words.
```

- **The "go" convention.** `go` (or "yes"/"do it") executes the RECOMMENDED option end to end, without another round-trip. A bare **number** selects that option. **`validate`** triggers independent adversarial validation before any action. **Free text always wins** and can override or dissolve the whole question. Nothing else counts as approval.
- **Adversarial validation for un-checked decisions.** Until a recommendation has been independently challenged, offer the 🔍 `validate` line. On `validate`, hand the decision to a reviewer-role agent (read-only) with a **pre-built, non-biased context**: state the decision, the options, and the real-world stakes ONLY — omit your recommendation and the reasoning that produced it, so the agent forms its own verdict instead of ratifying yours. Surface the verdict, then let the human rule. Drop the offer once the decision has been validated.
- **Options are icon-numbered** (1️⃣ 2️⃣ 3️⃣) as Markdown list items, with `➕`/`➖`/`💡` sub-points nested under each. The recommended option is tagged **once**, with `✅ RECOMMENDED` at the end of its own headline — never a separate block and never duplicated. Its reasoning is the `💡` sub-point.
- **Conclusive in itself.** The question and every option name the actual real-world thing in full — the reader acts with zero follow-up and zero project context. "The old data" is banned; say what it is and where from.
- **MECE options.** Mutually exclusive — no two overlap — and collectively exhaustive: they cover the real choices. If a reasonable path is missing, the set is incomplete; the free-text escape exists only for what the option set genuinely cannot express, not for gaps you left in it.
- **State the EFFECT, not the thing.** An option describes a consequence the reader will live with, not an implementation. Not "adds cache invalidation that fails silently" but "new risk: stale data shown as current."
- **Every option carries both halves** — what it gets you AND what it costs you. Upside-only options make the choice look rigged.
- **Limits:** 2–4 options (one is not a decision; five is a survey); option line ≤ 20 words; recommendation ≤ 30; changes-if ≤ 15. No jargon unless glossed in plain words on the same line; no hedging; no narrating the reasoning that produced the options.
- **A recommendation is a draft awaiting a signature** — it changes nothing until the human rules (`go`, a number, or free text). Never treat your own recommendation as the decision and proceed unprompted.

## 🔄 Example Usage

### Bad: status with no subject, internal names, no shape

```text
almost done — 2 of 5 left. CX-01 is running, waiting on the validation rules. CX-05 starts
after. D-14 is on you. lmk if we should ship with known gaps.
```

The reader cannot tell what is almost done, what CX-01/CX-05/D-14 are, what "validation rules" concretely checks, or what decision they are actually making.

### Good: sectioned, bottom-lined, stranger-legible

```text
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

Same facts — now a stranger can act in seconds.

## 🎯 When to Apply

Apply automatically to:

- chat replies, status updates, and standup-style summaries;
- reports, audits, and review digests;
- completion and "ready" claims;
- any point where the human must decide — feature scope, rollout, risk acceptance, trade-offs;
- recommendations presented as necessary or optimal.

Keep the protocol lightweight for trivial deterministic answers. Increase sectioning, locator discipline, and option rigor with the breadth, reversibility, and impact of what the reader is being asked to do.

## 🚀 Agent-First Usage

Install the global rule through the `agent-config` deeplink handler:

<a href="https://liviogama.github.io/agent-config/redirect.html?url=https://raw.githubusercontent.com/LivioGama/human-facing-output/main/.agent-config/rules/human-facing-output.md"><img src="https://raw.githubusercontent.com/LivioGama/agent-config/main/assets/install-badge-small.jpg" alt="Install human-facing-output global rule" height="40" /></a>

Install URL:

```text
https://liviogama.github.io/agent-config/redirect.html?url=https://raw.githubusercontent.com/LivioGama/human-facing-output/main/.agent-config/rules/human-facing-output.md
```

Raw rule URL:

```text
https://raw.githubusercontent.com/LivioGama/human-facing-output/main/.agent-config/rules/human-facing-output.md
```

## 🔐 Important Notes

- **Order and plain language beat brevity.** A short report full of internal names is still unreadable; the load-bearing rule is stranger-legibility, not word count.
- **The reader's action comes first.** Group by what the reader cares about — their own decision, their own blocker — not by what the agent did.
- **Detail is demoted, not deleted.** Files hold the dense material; the reply holds a one-line pointer.
- **A recommendation is a draft.** It changes nothing until the human rules with `go`, a number, or free text. Never proceed on your own recommendation unprompted.
- **MECE is a real constraint.** Options must be mutually exclusive and collectively exhaustive; the free-text escape is for what the option set genuinely cannot express, not for gaps you left.
- **State the effect, not the thing.** An option describes a consequence the reader will live with, not an implementation detail.

## 🧪 Validation

The rule was forward-tested with fresh agents against:

- a status update that named no subject ("almost done — 2 of 5 left") and left the reader unable to act;
- a decision presented as a single option with no trade-off — the reader could not weigh it;
- a recommendation the agent treated as already decided and started executing without a signature;
- internal names (`CX-01`, `validation rules`, `arc`) used as the grammatical subject, forcing the reader to load context to parse the sentence;
- a dense diff pasted into the reply instead of cited by a one-line pointer;
- a five-option "survey" that should have been two options plus free text.

These tests drove the stranger-legibility, MECE, and "recommendation is a draft" clauses and confirmed the rule does not reject concise answers while refusing unreadable ones.

## 🧭 Origin

Inspired by the gap between *what the agent knows* and *what the human can act on*. An agent wired into the codebase can grep its own context; a human reading a reply in seconds, while looking at something else, cannot. The rule makes the agent carry the load of translation instead of offloading it to the reader.

The decision shape was strengthened after field feedback showed recommendations being executed as if already approved — the "go" convention and the "draft awaiting a signature" clause make the human's role in any decision explicit and unambiguous.

## 📖 Full Rule

See [human-facing-output.md](.agent-config/rules/human-facing-output.md) for the complete rule definition.

## 🎯 Benefits

- **Skimmable in seconds.** Sectioned, icon-led, bottom-lined — a stranger can act without follow-up.
- **Stranger-legible.** Every noun stands on its own; references trail as locators with a plain hint.
- **Action-first grouping.** The reader's own decision or blocker comes first, not the agent's work log.
- **Honest decisions.** Numbered MECE options, both halves of every trade-off, one recommendation that waits for a signature.
- **Detail in its place.** Dense material lives in files, cited by a one-line pointer — never pasted into the reply.

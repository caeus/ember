# v3 — Evolutionary generation protocol

**User = fitness function. Agent = generator.**

The user scores. The agent never promotes a genome on its own judgement.

---

## The ladder

Genomes move **up** as they earn relevance. A genome's tier is simply which folder it
lives in.

```
v3/
├── canon.md            binding world rules
├── protocol.md         this file
├── events.md           candidates for consequential canonical events (NOT canon)
├── reveal-order.md     what the reader learns, and in what order
├── ancestors.md        pre-reset genetic material (not canon)
├── ledger.md           generation log + scores
├── 0-pool/             SUGGESTED — freshly generated, unscored
├── stashed/            PAUSED — unscored pool genomes held out of circulation
├── 1-kept/             SURVIVED — scored well enough to breed from
├── 2-developed/        LOAD-BEARING — expanded, placed in chronology
├── 3-spine/            COMMITTED — drafted prose, part of the book
└── graveyard/          REJECTED — with the reason, so we don't regenerate it
```

**Movement rules**

- Up one tier at a time. No skipping.
- Only the user promotes. The agent proposes.
- Demotion is allowed and cheap. A `2-developed` genome that stops working goes back to
  `1-kept` or to `graveyard`.
- A genome in `graveyard` keeps its file. The rejection reason is the most valuable thing
  in it — it stops the same idea being regenerated in three variants next round.
- Promotion **does not** rewrite the genome. Beats stay beats until `3-spine`, where a
  `draft.md` joins the genome file in a folder of its own.
- `stashed/` is **not** a tier or a verdict. Files there retain `status: pool` and remain
  unscored; they are simply outside active circulation until the user restores them.
  Do not treat stashing as rejection or promotion.

---

## Your notes in the files

You leave improvements inline, anywhere in any file, as:

```
[Note: what you want changed /]
```

**Agent procedure.** Before doing anything else in a session, sweep for them:

```
grep -rn "\[Note:" v3/ --exclude=protocol.md
```

Act on every one found. Then **delete the marker** — a note that has been handled must not
survive, or the next sweep can't tell done from pending. If a note can't be acted on, leave
it in place and say why.

Notes outrank anything the agent previously wrote in the same file. A note on a
`[PROPOSED]` block is a verdict on it.

---

## Event-shock proposals (a separate, nonbinding layer)

When the user asks what could happen next or later, propose **12 short candidate canonical
events** before generating more scenes. These are possible future *changes to the story's
history*, not additions to canon. This is a different lens from extrapolating current
threads or producing four more scene variants.

- Make **disruptions**, not just consequences of known plots: accidents, private crises,
  betrayals, irreversible decisions, institutional mistakes, unintended side effects and
  unlikely collisions.
- Each proposal must imply a causal chain: **event -> emotional disturbance -> believable
  (possibly irrational) decision -> lasting change in trajectory**.
- Make it concrete and actionable in one or two sentences; do not write a mini-plot.
- Vary the scale, chronology, characters and source of pressure. Some proposals can be
  wholly unrelated to the Field. Do not force convergence toward an assumed ending.
- Preserve the uncertainty of the Field and the embargo on its hidden mechanics. Expose
  conflicting values, not explanatory shortcuts.
- A proposal may be **favored** by the user without being canon. The agent may not turn
  approval, enthusiasm or a good genome into binding history. **Only an explicit user
  decision makes an event canon.**

Record selected ideas in `events.md`, with their status and any canon conflict.
`favored` means worth exploring, **not** accepted. `deferred` preserves a compelling
but costly possibility without forcing it into the narrative.

If the user wants scenes, transform selected event candidates into **one-scene, one-POV
genomes**, in normal four-genome generations under `0-pool/`. Each scene dramatizes one
choice or reversal; it must not summarize the entire event chain. Put broader consequences
in its Notes, and any assumed unclosed facts in `needs`. Genomes continue to require user
scoring and promotion through the existing ladder.

An explicitly accepted event belongs in `canon.md` as a binding history fact, and gets a
`reveal-order.md` row only if the reader must learn it at a particular point. Accepting an
event does **not** automatically promote its scene genomes.

---

## The scene is the atom

There is no layer **below** the scene. Scene execution remains atomic: a beat is
not a separate asset. A *candidate canonical event* in `events.md` sits **above**
scenes, as a possible change in story history, and is nonbinding until the user accepts it.
It is not a substitute for a scene and cannot be used as evidence of canon.

Outside those event-shock candidates, an idea worth keeping becomes **a scene**, **a rule
in `canon.md`**, or **a row in `reveal-order.md`**.

Unwritten scenes wait in the **backlog** at the top of `ledger.md`, one line each. A
backlog line is not an asset. It becomes real when a generation picks it up and it survives
scoring.

A fact the reader must learn needs a **position** in `reveal-order.md`. A reveal with no
position is just a fact, and facts without a position leak early.

---

## Generation rules

**Four genomes per generation.** Each genome is:

- **one scene**
- **one POV**
- simple
- short

A genome is **not** a miniature multi-scene plot wearing one scene's clothes. If beats
require a time jump or a second location, it is two genomes.

**Vary aggressively across the four** — POV, chronology, scale, narrative function. One
generation can hold something from inside Imogen's sleep, something months later, something
around Victoria, something near Hugo. Four cosmetic variants of one idea is a failed
generation.

**Every genome declares what it advances:**

| tag | advances |
|---|---|
| `WB` | worldbuilding |
| `INST` | institutional or societal response |
| `CHAR` | character development |
| `REL` | relationship |
| `PLOT` | causal / plot movement |
| `MYSTERY` | useful pressure without cheap revelation |

Prefer **observable situations and consequential choices** over exposition.

**Not every scene needs a clue.** A genome earns its place if it makes a character matter,
increases social pressure, introduces a misleading model, creates a relationship, gives an
anomaly emotional consequences, or establishes something that acquires new meaning after
Hugo's reveal.

---

## Hard constraints on generation

Carried from `canon.md`, repeated because they are the ones most easily broken:

1. **Semantic, not sensory.** No transmitted scenery. All imagery is the recipient's
   rendering.
2. **No convergent renderings.** Two characters never describe the same dream place.
3. **No cheap discovery.** See `canon.md` §3 for the banned-moves list.
4. **No puppeteering.** Victoria, Clement and Hugo's actions and interiors are off-limits
   outside their own POV scenes. In another POV they may only be *observed*.
5. **Don't close an `[OPEN]`.** If a genome needs one closed, it says so in its
   `needs` field rather than assuming.

---

## Genome file format

One file per genome. Filename `G###-slug.md`. The ID never changes as the genome moves up.

```markdown
---
id: G001
title: The Same Hour
pov: <character, and their relation to the case>
when: <position in chronology, relative — not a date>
advances: [MYSTERY, CHAR]
status: pool | kept | developed | spine | graveyard
parents: []          # genome IDs this was mutated from, or the backlog line it came from
needs: []            # [OPEN] canon points this genome would force closed
---

**Logline.** One sentence.

**Beats**

1. ...

**Notes** — what it sets up, what it recontextualizes after Hugo's reveal, what it
deliberately withholds.
```

---

## Scoring

The user scores each genome in `ledger.md`. Suggested axes, used loosely:

- **Pressure** — does it make the world heavier?
- **Honesty** — does it earn what it reveals?
- **Consequence** — does anything become true that wasn't before?
- **Voice** — is this a scene someone would want to read?

A score is not a number unless the user wants numbers. "Keep", "kill", "keep but not like
this" is enough to breed from.

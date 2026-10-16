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
├── reveal-order.md     what the reader learns, and in what order
├── ancestors.md        pre-reset genetic material (not canon)
├── ledger.md           generation log + scores
├── 0-pool/             SUGGESTED — freshly generated, unscored
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

## The scene is the atom

There is no layer below the scene. If something is worth having it is **a scene**, **a rule
in `canon.md`**, or **a row in `reveal-order.md`**. Nothing floats in between.

An idea that cannot be made into a scene is either a rule — in which case it belongs in
canon, where it binds every scene — or it is nothing, and finding that out early is the
point of the constraint.

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
title: Hugo at the Bedside
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

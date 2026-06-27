# grain-skills

Open verification skills for **Grain** — the deterministic verify-and-settle layer for 3D assets.

Grain grades a 3D asset (GLB) against an **acceptance profile** and returns a **signed, settleable
verdict**: a per-predicate PASS/FAIL plus a `predicateDigest` that commits to the result, so the same
bytes against the same profile always grade identically. Agents and humans can call it in the loop; a
marketplace or escrow can settle on the verdict.

Grain **verifies**; it never generates. Bring assets from any source — Blender, an AI generator
(Tripo, Meshy, Hunyuan), a marketplace download — and Grain tells you, byte-bound and signed, whether
they meet the bar.

## What's open vs. what's private

This repo is the **method**, and it is deliberately, fully open:

- the **predicate vocabulary** — what Grain measures
- the **profile schema** — how an acceptance bar is composed
- the **verdict + digest format** — what a grade commits to
- the **workflow-digest** memory format — how a verified workflow becomes a reusable recipe
- a public **test corpus** and a reproducible **benchmark**

The **tuned thresholds** that turn this vocabulary into a specific buyer's acceptance bar are **not**
here. They live in a private profile store (the `ProfileResolver` seam) and are referenced only by id.
Open the method; keep the moat. Same engine, two runtimes — Mind-equip on the Bazaar is the *money*
runtime; this repo is the *trust* runtime.

## Skills

| Skill | What it does |
|---|---|
| [`grain-3d-grader`](skills/grain-3d-grader) | Grade a GLB against a profile → per-predicate verdict + signed commitment |
| [`grain-conform`](skills/grain-conform) | Repair a GLB to watertight / on-budget, then re-grade |
| [`grain-acceptance-profile`](skills/grain-acceptance-profile) | The profile schema — compose an acceptance bar from predicates |
| [`grain-workflow-digest`](skills/grain-workflow-digest) | Turn a verified workflow into a reusable, shareable recipe |
| [`grain-settle`](skills/grain-settle) | Settle escrow on a signed verdict |

Root onboarding + auth: [`SKILL.md`](SKILL.md) (also intended to be served at
`https://grainbygrain.xyz/SKILL.md`).

## For Minds (the Bazaar)

The consumer-facing artifact is a single equippable skill — **"Grain — 3D Asset Verifier"** — that
wraps grade + conform + profile. This repo is the technical source of truth; the Bazaar listing is the
equip surface.

## Versioning & license

Each skill is versioned independently (`version` + `updated` in its frontmatter). MIT — see
[LICENSE](LICENSE).

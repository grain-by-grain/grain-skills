---
name: grain
description: Verify a 3D asset against an acceptance profile and get a signed, settleable verdict — deterministic 3D verification, in the loop.
version: 0.1.0
updated: 2026-06-27
homepage: https://grainbygrain.xyz
env:
  - GRAIN_SERVICE_URL   # base URL of the Grain service (default: https://grainbygrain.xyz/api)
  - GRAIN_API_KEY       # sent as x-grain-key, only if the service is gated
---

# Grain

Grain is a **deterministic verify-and-settle layer for 3D assets**. It grades a GLB against an
**acceptance profile** and returns a **signed verdict** — a per-predicate PASS/FAIL and a
`predicateDigest` that commits to the result. Identical bytes against the same profile always produce
the same digest, so the verdict is reproducible and settleable across a trust boundary.

Grain **verifies**; it never generates. Bring assets from any source — Blender, an AI generator
(Tripo, Meshy, Hunyuan), a marketplace download — and Grain tells you, byte-bound and signed, whether
they meet the bar.

## Connect

Point at the hosted service or your own:

- `GRAIN_SERVICE_URL` — default `https://grainbygrain.xyz/api`
- `GRAIN_API_KEY` — sent as `x-grain-key` (only if the service is gated)

## Skills

- **grain-3d-grader** — grade a GLB → verdict
- **grain-conform** — repair → re-grade
- **grain-acceptance-profile** — compose an acceptance bar
- **grain-workflow-digest** — remember a verified workflow as a recipe
- **grain-settle** — settle escrow on a verdict

## The boundary

The predicate vocabulary and every format in this repo are open. The **tuned thresholds** that define a
specific buyer's bar are private and referenced by profile id. Grade against your own profile by
passing a plan directly, or against a buyer's published profile by id.

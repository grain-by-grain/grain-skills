---
name: grain-acceptance-profile
description: The acceptance-profile schema — compose a 3D acceptance bar from public predicates. Threshold values stay private.
version: 0.1.0
updated: 2026-06-27
---

# grain-acceptance-profile

An **acceptance profile** is the bar a buyer accepts. It selects predicates from the public vocabulary
and parametrizes each with a threshold. The **schema is open; the threshold values are the moat** and
are not published — a profile is referenced by id and resolved from a private store at grade time.

## Schema (a `GradePlan`)

```json
{
  "profileId": "game-ready-prop@1",
  "mode": "all",                 // "all" = every predicate must pass; "weighted" = score >= minScore
  "minScore": 1.0,               // weighted mode only (0..1)
  "format": "glb",               // required container
  "entries": [
    { "id": "tri_count",    "threshold": { "max": 10000 }, "weight": 1 },
    { "id": "manifold",     "threshold": { "watertight": true } },
    { "id": "uv_present",   "threshold": { "required": true } },
    { "id": "texture_size", "threshold": { "max": 2048 } }
  ]
}
```

`id` must exist in the predicate registry (`tri_count`, `manifold`, `valid_glb`, `named_params`,
`file_size`, `uv_present`, `texture_size`, `dimensions`). `threshold` is the per-buyer secret — the
values above are **illustrative**, not a real buyer's bar.

## Resolving

Public grader code depends only on a resolver: `ProfileResolver(profileId, buyer) -> GradePlan`. With
no resolver registered you pass a `GradePlan` directly (your own bar, or tests). A buyer's tuned bar
resolves from their private store and never appears in any open file.

See [schemas/profile.schema.json](../../schemas/profile.schema.json).

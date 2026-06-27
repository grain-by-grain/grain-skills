---
name: grain-workflow-digest
description: Turn a creator's verified workflow into a reusable, shareable recipe — the "remember" half of watch → verify → remember.
version: 0.1.0
updated: 2026-06-27
---

# grain-workflow-digest

When a creator's pipeline produces an asset that **passes** Grain, the workflow that produced it is
worth remembering. A companion logs events locally (free), detects when a workflow is **stable**, and
emits one session-end digest. A Mind promotes a stable digest to a durable **recipe** — a named,
forkable template of a proven, verified pipeline.

## `recipe.workflow-digest-v1`

```json
{
  "schema_version": 1,
  "session_id": "<opaque>",
  "events": [
    {
      "recipe_shape_id": "blender-character-export",
      "asset_kind": "character",
      "grading_profile": "game-ready-prop@1",
      "pass": true,
      "predicate_digest": "<from the verdict>",
      "tool": "blender",
      "stage": "export",
      "at": 1750000000
    }
  ],
  "aggregates": {
    "blender-character-export|game-ready-prop@1|character": {
      "count": 4, "pass_count": 4, "pass_rate": 1.0, "distinct_asset_count": 3, "stable": true
    }
  }
}
```

**Stability** = 3+ identical PASS on the `(recipe_shape_id, grading_profile, asset_kind)` triple. The
companion pre-computes it; the Mind promotes to a `tenet` lesson when
`distinct_asset_count >= 2 AND pass_rate >= 0.8 AND count >= 3`, and authors a named recipe artifact
(e.g. `recipe.blender-character-export-v1`).

The companion is cheap local signal-detection; the Mind is the expensive central interpret-and-store.
**Privacy:** only derived events (stage + profile + verdict) are promoted — never raw screen capture,
keystrokes, or source files.

See [schemas/digest.schema.json](../../schemas/digest.schema.json).

## Publish & share — a forkable recipe template

A promoted recipe is published as a **`recipe.workflow-template-v1`** — an immutable JSON artifact
(`nodes[] + edges[] + provenance`) that is the source of truth, wrapped as a **listed Skill** so others
can discover and adopt it. The body carries its own provenance: the verifying mind, an immutable
`verification_snapshot` (the authorizing digest's aggregates + `predicate_digests` + a `snapshot_hash`),
and `verified_under` (which `grading_profile` × `asset_kind` it is proven for). So an adopter sees
*"verified for profile P on stylized_character — 4 PASS / 0 FAIL across 3 distinct assets as of <date>"*,
not just steps.

**The verified claim dies at the first fork — by design.** Adopters **clone, never mutate** the
original. A fork carries `forked_from` and a `drift_status` of `unverified-fork-*` until it re-earns
the claim by passing the same stabilization rule on the forker's own assets. The `snapshot_hash` makes
the original tamper-evident: edit the snapshot and the hash no longer matches, voiding the claim. A
"verified" signal that survives edits because someone asserts a fork is faithful is exactly the kind of
trust that erodes — drift honesty is the feature, not a tax.

See [schemas/recipe-template.schema.json](../../schemas/recipe-template.schema.json).

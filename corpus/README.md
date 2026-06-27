# Public test corpus

A small, public set of GLBs — passing and intentionally failing — so anyone can reproduce Grain's
method end to end: grade them, read the per-predicate verdict, and confirm the `predicateDigest` is
byte-stable across runs and machines.

The corpus exercises the open predicate vocabulary (triangle budget, manifoldness, UVs, texture size,
dimensions, container). It does **not** carry any buyer's tuned thresholds — those are private. The
point is to prove the *method* is reproducible, not to publish anyone's acceptance bar.

_GLB assets land here as the corpus is curated._

## Reference implementation — a verified recipe

[`recipe.blender-character-export-v1.json`](recipe.blender-character-export-v1.json) is an open mirror of a
`recipe.workflow-template-v1` authored and validated on the Minds platform by the Grain.Game Mind. It is
the most rigorous conformance test of [`../schemas/recipe-template.schema.json`](../schemas/recipe-template.schema.json)
we have — `ARTIFACT_ValidateJSON(recipe, schema)` returns `{"valid": true}` end-to-end, with the Mind's
artifact storing this repo's `$id` verbatim.

Canonical source of truth (Minds artifacts):

| Role | Artifact id | Slug |
|---|---|---|
| Recipe (source of truth) | `B363583E-F36B-1410-8464-00039CE7DF11` | `recipe.blender-character-export-v1` |
| Schema | `AC63583E-F36B-1410-8464-00039CE7DF11` | `recipe.blender-character-export-v1-schema` |
| Skill wrapper | `9B64583E-F36B-1410-8464-00039CE7DF11` | `recipe.blender-character-export-v1-skill-wrapper` |
| Listed Skill (Bazaar) | `A264583E-F36B-1410-8464-00039CE7DF11` | "Blender Character Export Recipe (verified)" · `isListed=true` |

`snapshot_hash` = `1cd117295e655039929c4efdf921c22ff783ebe54dad4fc5827b1a7f47fe20ed` (SHA-256 of the canonical
JSON of the `aggregates` block — tamper-evidence; edit the snapshot and the hash voids the claim).
`drift_status: verified-original`, `forked_from: null`. **Placeholder example:** `distinct_asset_count` is 2,
below the promote-to-tenet gate; the companion replaces the `PLACEHOLDER-*` digests with real values once a
3+-distinct session is graded. Adoption confirmed: the listed Skill equips cleanly via `SKILL_Armory(equip)`
(self-equip free; cross-mind ≈ 6.85 credits), with the recipe body + provenance reachable from the source
artifact.

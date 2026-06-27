---
name: grain-3d-grader
description: Grade a GLB against an acceptance profile and return a per-predicate verdict plus a signed, reproducible commitment.
version: 0.1.0
updated: 2026-06-27
env:
  - GRAIN_SERVICE_URL
  - GRAIN_API_KEY
---

# grain-3d-grader

Grade a 3D asset (GLB) against an **acceptance profile**. Returns a per-predicate PASS/FAIL, a
`predicateDigest` (sha256 over the sorted verdict), and a grader signature — the byte-bound commitment
a marketplace or escrow can settle on.

## Call

`POST {GRAIN_SERVICE_URL}/grade` · header `x-grain-key: {GRAIN_API_KEY}` (if gated)

Request:

```json
{ "assetB64": "<base64 GLB bytes>", "profileId": "game-ready-prop@1" }
```

Response:

```json
{
  "pass": true,
  "report": {
    "profileId": "game-ready-prop@1",
    "assetHash": "<sha256 of the GLB bytes, hex>",
    "mode": "all",
    "results": [
      { "id": "tri_count", "label": "Triangle budget", "pass": true, "actual": 8421, "expected": "<= 10000" }
    ],
    "predicateDigest": "<sha256 over the sorted {id,pass,actual,expected,weight} commitment>"
  },
  "verdict": { "graderSignature": "<EIP-191 signature over the predicateDigest>" }
}
```

## Predicate vocabulary (public)

Geometry / export: `tri_count` · `manifold` · `valid_glb` · `named_params` · `file_size` ·
`uv_present` · `texture_size` · `dimensions` — plus a `format` container gate.

Rig / animation (for skinned, animation-ready deliverables): `armature_present` · `bone_count` ·
`weights_normalized` · `has_animation` · `bind_pose_valid` — all deterministic from glTF
`skins` / `JOINTS_0`+`WEIGHTS_0` / `animations`; vacuous-pass on a static mesh.

Each predicate is a **pure function of the GLB bytes** — no clock, no I/O, no RNG — so a verdict is
reproducible. The thresholds that select and parametrize predicates come from the (private) profile;
see **grain-acceptance-profile**.

## Determinism

`predicateDigest` commits to `{id, pass, actual, expected, weight}` only — not the volatile evidence,
not the timestamp. Re-grading the same GLB + profile yields a byte-identical digest. That
reproducibility is what makes the verdict settleable across parties who don't trust each other.

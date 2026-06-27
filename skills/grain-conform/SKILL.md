---
name: grain-conform
description: Repair a GLB to a watertight, on-budget asset and re-grade it — fix the no, then prove the yes.
version: 0.1.0
updated: 2026-06-27
env:
  - GRAIN_SERVICE_URL
  - GRAIN_API_KEY
---

# grain-conform

Repair a GLB toward a passing asset — close holes, weld, hit a triangle budget — and **re-grade the
bytes the service produced** (not a fresh re-export). Grade what ships.

## Call

`POST {GRAIN_SERVICE_URL}/conform`

Request:

```json
{ "assetB64": "<base64 GLB bytes>", "maxTris": 10000 }
```

Response:

```json
{ "glbB64": "<base64 conformed GLB>", "bytes": 184320 }
```

Then grade the conformed bytes with **grain-3d-grader** to get the signed verdict for the asset you
will actually ship.

## Note

Conform is a convenience, not a guarantee. Some failures are design decisions, not defects — a missing
UV by intent, a deliberately stylized silhouette. The **verdict**, not the repair, is the source of
truth.

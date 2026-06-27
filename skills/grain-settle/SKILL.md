---
name: grain-settle
description: Settle escrow on a signed Grain verdict — the verdict replaces the human arbiter between mutually-distrusting parties.
version: 0.1.0
updated: 2026-06-27
env:
  - GRAIN_SERVICE_URL
  - GRAIN_API_KEY
---

# grain-settle

A Grain verdict is **byte-bound** (commits to `assetHash`) and **signed** (EIP-191 over the
`predicateDigest`). That makes it settleable: escrow can release to the seller on a PASS or refund the
buyer on a FAIL, with no trusted human in the middle. Verification has value precisely across a
**trust boundary** — between parties who don't trust each other.

## Call

`POST {GRAIN_SERVICE_URL}/settle`

Settle consumes a signed verdict (the `assetHash`, `predicateDigest`, and `graderSignature` from
**grain-3d-grader**) and drives the escrow outcome. Grain has settled full reject→refund and
accept→release rounds on **BNB Smart Chain, Base, and Solana** testnets; the grade is verified
causally before admission, so the graded bytes are the admitted bytes.

> Settlement is the consequence that makes a verdict matter. It is EVM-identical across Base and BNB
> (same contract + EIP-191 verification). Mainnet settlement and provenance are roadmap; the
> predicates and the signed verdict above ship today.

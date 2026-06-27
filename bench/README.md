# Reproducible benchmark

"Here is exactly how Grain grades" — a harness that runs the predicate vocabulary over the public
[corpus](../corpus) and reports per-predicate results and timing, so the method is **measurable and
auditable** rather than asserted.

Deterministic by construction: predicates are pure functions of the GLB bytes (no clock, no I/O, no
RNG), so the same corpus + profile produces the same verdicts and the same digests anywhere.

_Harness lands here; it mirrors the grader's internal benchmark._

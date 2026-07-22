---
name: finalize
description: Fourth and final phase. Evaluate the best model on the held-out test set, decide whether to return to Iterate or accept results, and record the final outcome in CONTEXT.md.
entry: User satisfied with validation performance; CONTEXT.md has pointer to best model
exit: CONTEXT.md updated with final decision, test metrics, and key handoff details.
---

# Phase 4 — Finalize

---

## Steps

### 1. Restore context
Read `CONTEXT.md` to identify the best model path and its validation performance.

### 2. Final test-set evaluation
Evaluate the best model on `test.X`. Report all metrics defined in Phase 1 (including run-time and memory).

### 3. Decide
- If test performance is significantly worse than validation: discuss with the user whether to return to Phase 3 — Iterate. **If you do, do not keep re-evaluating on the same test set** — each repeated peek erodes its independence and reintroduces the overfitting the holdout was meant to catch. Advise the user to gather fresh data for a new test set before iterating further.
- If test performance is acceptable: finalize.

## Context dump (end of phase)

Complete the Phase 4 — Finalize section of `CONTEXT.md` with:
- Final decision and selected model path;
- Concise usage entry point;
- Final validation and test metrics, including runtime and memory;
- Interpretation of the validation-to-test difference;
- Acceptance-criteria results;
- Most important limitations.

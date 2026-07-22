# Checklist for automodel

Progress tracker — copy to project root and update as you complete each step.

## Phase 1 — Setup
- [ ] Goal, data, metrics, and optimization routine reviewed with user
- [ ] Selection principle agreed; train / validation / test splits created (validation optional if selecting on a penalised in-sample score)
- [ ] `CONTEXT.md` created; compact if under context pressure

## Phase 2 — Baseline Model
- [ ] Mock model implemented; end-to-end pipeline verified by a sub-agent
- [ ] `CONTEXT.md` updated with baseline metrics; compact if under context pressure

## Phase 3 — Iterate
- [ ] M, S, I chosen with user
- [ ] Meta-iteration 1 complete; `CONTEXT.md` updated; compact if under context pressure
- [ ] *(repeat for each subsequent meta-iteration)*
- [ ] Progress reviewed with user; `CONTEXT.md` updated with best model pointer; compact if under context pressure

## Phase 4 — Finalize
- [ ] Best model evaluated on test set
- [ ] Final decision, test metrics, and limitations recorded in `CONTEXT.md`

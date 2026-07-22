---
name: setup
entry: No `CONTEXT.md` artifact in project root folder
exit: Set up completed and documented in CONTEXT.md.
description: First phase. Confirm goal and terminology, prepare data splits, define loss/metrics, and set up parameter optimization.
---

# Phase 1 — Setup

---

## Steps

### 0. Feasibility
- Confirm that subagents can be spawned and read, write, and execute files in the project directory (and subdirectories)
- Confirm with the user their intended language/runtime and that required libraries are available

### 1. Goal
Confirm with the user:
- Check for any useful info in the skill's `references` folder
- Context, intended goal, and scope of the model
- Domain lingo to use throughout (e.g. *loss function* vs. *cost function* / *features* vs. *covariates* / *training* vs. *calibration*)
- Whether the model needs to meet certain properties (e.g. differentiability, positivity, boundedness, some equivariance, adhere to some physical constraints, etc.)

### 2. Existing code
If code already exists, review it with the user and decide whether to reuse or rewrite. Use these skip signals: if train/val/test split files exist, skip to Metrics; if an optimization routine exists, skip to the context dump.

### 3. Data
Identify and confirm:
- Where the data lives and which files/tables are relevant
- Intended input and output variables
- Whether data is present, sufficient, and clean; flag any cleaning needs
- A split strategy for `train.X`, `validation.X`, and `test.X` (e.g. `.csv`, `.mat`, `.rdata`), stored in a consistent location. Confirm with the user:
  - **Selection principle.** Default to a held-out validation set (optionally *k*-fold cross-validation for a less noisy estimate). If the selection metric *already* penalises complexity — an information criterion such as AIC/BIC/MDL — the penalised in-sample score can serve instead, and a validation split may be unnecessary: the penalty is what guards against overfitting. The user may override either way. Keep a held-out **test** set regardless, as a final check. Record the choice in `CONTEXT.md`, since later phases score every candidate against it.
  - **Leakage.** Guard against it when splitting: group/entity leakage (e.g. repeat measurements from one patient landing in different splits), time-series autocorrelation across split boundaries, and duplicate rows.

### 4. Metrics
Define and confirm with the user:
- Objective/loss function for training/calibration
- Evaluation metrics for the validation and test sets
- *Always include run-time and memory usage as metrics* — these gate the feasibility of the iterative loop
- If applicable (e.g. searching for equations, not neural architectures), include parsimony pressure — either within the loss in consultation with the user, or at least reported per attempt (e.g. AIC/BIC/MDL) — so the search does not silently drift toward ever more complex models

See `TIPS.md` in the skill root for optional practices best decided here: attaching uncertainty to metrics, controlling optimizer noise, and recording trivial baselines for context.

### 5. Optimization routine
Implement a parameter optimization routine, or confirm an existing one, e.g. gradient descent or a black-box method (PSO, Nelder-Mead). Prefer libraries over from-scratch implementations.

---

## Context dump (end of phase)

Create `CONTEXT.md` in the project root using `assets/CONTEXT.md` as a starting point. Fill in the Phase 1 sections:
- Goal and scope
- Language/runtime and key libraries
- Data location, variable names, split strategy
- Chosen loss/cost/objective function and evaluation metrics
- Brief description of the optimization routine

Then **verify `CONTEXT.md` is self-sufficient**: a fresh agent with no conversation history should be able to resume from it alone. This is the real requirement — the durable state lives in `CONTEXT.md`, not in the conversation.

**Compact the conversation history under context pressure** — e.g. this phase left large data or tool-output dumps in context, or the window is visibly filling. Otherwise proceed directly to Phase 2 — Baseline Model.

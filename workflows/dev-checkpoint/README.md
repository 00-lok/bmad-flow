# Dev Checkpoint

> Reconcile your BMAD planning artifacts with the reality of your codebase.

## The Problem

During development, your BMAD artifacts (PRD, architecture, stories...) inevitably drift from your actual code. Features get added that aren't documented. Architecture decisions change without updating the docs. Stories are implemented differently than planned.

This drift degrades your AI-assisted development because the AI works with outdated context that no longer reflects the real project.

## What This Workflow Does

**Dev Checkpoint** performs a full reconciliation in 7 steps:

```
Step 1  ─ Initialize     Detect artifacts, gather context, create checkpoint folder
Step 1b ─ Continue        Resume a previous session (if interrupted)
Step 2  ─ Code Analysis   Deep autonomous scan of your entire codebase
Step 3  ─ Artifact Review Read and evaluate every BMAD planning artifact
Step 4  ─ Diagnostic      Compare code vs. artifacts — identify all misalignments
Step 5  ─ Decisions       Collaboratively decide: update docs OR fix code
Step 6  ─ Application     Apply doc updates to artifacts + compile code action items
Step 7  ─ Snapshot        Generate a human-friendly project health summary
```

### What You Get

A timestamped checkpoint folder with:

| File | Description |
|------|-------------|
| `checkpoint-summary.md` | Human-friendly project overview with health score |
| `codebase-analysis.md` | Full code review (structure, quality, tech debt) |
| `artifacts-review.md` | Review of every BMAD artifact |
| `misalignment-report.md` | Every divergence between plan and reality |
| `decisions-log.md` | Your decisions on how to handle each divergence |
| `action-items.md` | Prioritized list of code corrections to plan |

Plus: **your BMAD artifacts are updated in-place** to reflect reality.

## Installation

### 1. Copy to Your Project

```bash
cp -r dev-checkpoint/ your-project/_bmad/bmm/workflows/4-implementation/dev-checkpoint/
```

### 2. Verify Config

Your `_bmad/bmm/config.yaml` should include these variables:

```yaml
project_name: "Your Project"
output_folder: "_bmad-output"
user_name: "Your Name"
communication_language: "fr"    # or "en"
document_output_language: "fr"  # or "en"
```

### 3. Launch

```
/bmad-bmm-dev-checkpoint
```

Or in natural language:
```
"Run dev checkpoint"
"Faire un point de dev"
```

## How It Works

### Phase 1: Initialization (Step 1)

The workflow:
- Scans your project for existing BMAD artifacts (PRD, architecture, stories, etc.)
- Asks you 2-3 targeted questions about recent changes
- Creates a timestamped checkpoint folder

### Phase 2: Analysis (Steps 2-3) — Autonomous

The AI performs deep analysis without needing your input:
- **Step 2**: Scans your entire codebase — structure, code quality, dependencies, git history, tech debt
- **Step 3**: Reads and evaluates every BMAD artifact — completeness, clarity, internal coherence

### Phase 3: Diagnostic (Step 4) — Autonomous

The AI cross-references code and artifacts to identify every misalignment, categorized by:
- **Architecture** — Structural divergences
- **Functional** — Feature coverage gaps
- **UX/UI** — Design divergences
- **Tech/Stack** — Technical choice differences
- **Documentation** — Incomplete or outdated artifacts

Each misalignment is rated:
- **Red** — Critical, needs immediate attention
- **Yellow** — Important, should be addressed
- **Green** — Minor, low impact

### Phase 4: Decisions (Step 5) — Collaborative

For each misalignment, you choose:
- **[D] Update Documentation** — The code is right, update the artifact
- **[C] Code Action** — The doc is right, note a fix for the code

Critical items are reviewed one by one. Minor items can be batch-processed.

### Phase 5: Application (Step 6) — Autonomous

The AI:
- Updates your BMAD artifacts in-place based on your [D] decisions
- Verifies cross-artifact coherence after changes
- Compiles all [C] decisions into a prioritized action items list

### Phase 6: Snapshot (Step 7) — Autonomous

A human-friendly summary is generated with:
- Project health score (green/yellow/red)
- Plain-language project state overview
- What was realigned
- What remains to be done
- Recommended next priorities

## Resumability

The workflow tracks progress via `stepsCompleted` in the checkpoint frontmatter. If your session ends mid-workflow:

1. Re-launch the workflow
2. It detects the in-progress checkpoint
3. Automatically resumes at the next step

## When to Use

- After a significant development phase
- When you feel your planning docs are outdated
- Before starting a new sprint or feature set
- When onboarding someone to understand project state
- Periodically (e.g., every 2-4 weeks of active development)

## Module Info

- **Module**: BMM (Software Development)
- **Phase**: 4-implementation
- **Session Type**: Continuable
- **Language**: Bilingual (FR/EN, follows your config)

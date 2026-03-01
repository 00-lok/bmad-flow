# Understanding BMAD Workflow Architecture

This document explains how BMAD workflows are structured so you can understand, modify, or create your own.

## Core Concepts

### Micro-File Architecture

BMAD workflows use a **micro-file design** where each step is a self-contained instruction file. This means:

- The AI only loads **one step at a time** (just-in-time loading)
- Each step file contains everything needed to execute that step
- Steps execute in strict order — no skipping or reordering
- Progress is tracked in output file frontmatter

### Why Micro-Files?

1. **Context efficiency** — AI models have limited context windows. Loading one step at a time keeps the context focused
2. **Resumability** — If a session ends, the workflow can resume at the last completed step
3. **Clarity** — Each step has a clear, bounded goal
4. **Maintainability** — Steps can be updated independently

## File Structure

Every BMAD workflow follows this structure:

```
workflow-name/
├── workflow.md              # Entry point — defines goal, role, and rules
├── workflow-plan.md         # Design document (optional, for transparency)
├── data/                    # Templates, schemas, reference data
│   └── template.md
└── steps-c/                 # Step files (c = create mode)
    ├── step-01-init.md      # Always starts with initialization
    ├── step-01b-continue.md # Continuation handler (for resumable workflows)
    ├── step-02-*.md         # Subsequent steps
    ├── step-03-*.md
    └── ...
```

### Folder Naming: `steps-c/`, `steps-u/`, `steps-d/`

BMAD supports three lifecycle modes:

| Folder | Mode | Description |
|--------|------|-------------|
| `steps-c/` | **Create** | Steps for creating something new |
| `steps-u/` | **Update** | Steps for modifying existing work |
| `steps-d/` | **Delete** | Steps for removing or archiving |

Most workflows only use `steps-c/`. Tri-modal workflows include all three.

## Anatomy of `workflow.md`

The entry point file contains:

```markdown
---
name: Workflow Name
description: What this workflow does
web_bundle: true
---

# Workflow Name

**Goal:** [Clear statement of what the workflow achieves]

**Your Role:** [How the AI should behave during this workflow]

## WORKFLOW ARCHITECTURE
[Core principles and rules]

## INITIALIZATION SEQUENCE
[How to start — load config, execute first step]
```

### Key Sections

- **Goal** — What the workflow produces and why
- **Your Role** — Persona and expertise the AI adopts
- **Core Principles** — Rules the AI must follow (micro-file design, sequential enforcement, etc.)
- **Critical Rules** — Non-negotiable constraints (never load multiple steps, always wait for user input at menus, etc.)
- **Initialization Sequence** — Config loading and first step execution

## Anatomy of a Step File

Each step file follows a consistent structure:

```markdown
---
name: 'step-XX-name'
description: 'What this step does'
nextStepFile: './step-XX+1-name.md'
checkpointFolder: '{checkpointFolder}'
---

# Step X: Title

## STEP GOAL:
[Clear statement of this step's objective]

## MANDATORY EXECUTION RULES (READ FIRST):
### Universal Rules:    [Rules that apply to all steps]
### Role Reinforcement: [Persona reminders]
### Step-Specific Rules: [Rules unique to this step]

## EXECUTION PROTOCOLS:
[How to execute this step]

## CONTEXT BOUNDARIES:
[What information is available and what's off-limits]

## MANDATORY SEQUENCE
[Numbered sequence of actions — follow exactly]

### 1. [First Action]
### 2. [Second Action]
...

### N. Present MENU OPTIONS
Display: **[C] Continue — [description]**

## SYSTEM SUCCESS/FAILURE METRICS
### SUCCESS: [What constitutes success]
### FAILURE: [What constitutes failure]
```

### Key Elements

| Element | Purpose |
|---------|---------|
| **Frontmatter** | Metadata: name, description, next step path, variables |
| **Step Goal** | Single clear objective for this step |
| **Execution Rules** | Constraints the AI must follow |
| **Context Boundaries** | What data is available vs. off-limits |
| **Mandatory Sequence** | Exact actions in order — the core of the step |
| **Menu** | User control point — workflow halts here |
| **Success/Failure Metrics** | How to evaluate if the step was done correctly |

## State Management

Workflows track progress using **frontmatter in output files**:

```yaml
---
stepsCompleted: ['step-01-init', 'step-02-analysis']
lastStep: 'step-02-analysis'
status: IN_PROGRESS
---
```

- `stepsCompleted` — Array of completed step names
- `lastStep` — Most recently completed step
- `status` — `IN_PROGRESS` or `COMPLETE`

This enables **session resumption**: if the workflow is interrupted, `step-01b-continue.md` reads the frontmatter and routes to the next step.

## Variable Resolution

Step files use variables that are resolved from the BMAD config:

| Variable | Source | Example |
|----------|--------|---------|
| `{project-root}` | Auto-detected | `/home/user/my-project` |
| `{project_name}` | `config.yaml` | `My App` |
| `{output_folder}` | `config.yaml` | `_bmad-output` |
| `{user_name}` | `config.yaml` | `John` |
| `{communication_language}` | `config.yaml` | `fr` |
| `{checkpointFolder}` | Set during step-01 | `_bmad-output/dev-checkpoints/2026-02-28T14-30-00` |

## Menu System

Every step ends with a menu that halts execution:

```markdown
### Present MENU OPTIONS

Display: **[C] Continuer — Lancer l'analyse**

#### Menu Handling Logic:
- IF C: verify outputs, load and execute next step
- IF Any other: help user, redisplay menu
```

The AI **must halt and wait for user input** at menus. This gives you control over pacing.

Common menu options:

| Option | Meaning |
|--------|---------|
| `[C]` | Continue to next step |
| `[A]` | Advanced elicitation (deeper exploration) |
| `[P]` | Party mode (creative brainstorming) |

## Subprocess Optimization

Some steps can leverage **sub-agents** for parallel processing:

```markdown
- Subprocess Pattern 2: One sub-agent per item (e.g., one per artifact)
- Subprocess Pattern 4: Parallel comparisons by category
- Fallback: Sequential processing in main thread
```

If the AI doesn't have sub-agent capabilities, it falls back to sequential processing. The workflow handles this gracefully.

## Creating Your Own Workflow

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines on creating and submitting new workflows.

Key principles:

1. **One goal per workflow** — Keep it focused
2. **Micro-file steps** — One concern per step file
3. **Clear boundaries** — Each step knows what it can and can't do
4. **User control** — Menus at every transition point
5. **State tracking** — Enable resumability
6. **Graceful fallbacks** — Work with or without sub-agents

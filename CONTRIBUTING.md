# Contributing

Thank you for your interest in contributing custom BMAD workflows! This guide explains how to submit your own workflow to this collection.

## Before You Start

Make sure your workflow:

1. **Solves a real problem** — It should address a gap in the standard BMAD toolkit
2. **Is reusable** — It should work on any BMAD project, not just your specific one
3. **Follows BMAD conventions** — Uses the micro-file architecture, state tracking, and menu system
4. **Is tested** — You've used it successfully on at least one project

## Workflow Requirements

### File Structure

Your workflow must follow this structure:

```
your-workflow/
├── README.md                # Required — documentation for users
├── workflow.md              # Required — entry point
├── workflow-plan.md         # Recommended — design rationale
├── data/                    # Optional — templates, schemas
│   └── ...
└── steps-c/                 # Required — step files
    ├── step-01-init.md
    ├── step-01b-continue.md # Required if continuable
    ├── step-02-*.md
    └── ...
```

### README Requirements

Your workflow README must include:

- **The Problem** — What problem does this solve?
- **What It Does** — Step-by-step overview
- **What You Get** — Output files and their purpose
- **Installation** — How to add it to a project
- **How to Launch** — Command to run it
- **When to Use** — Scenarios where this workflow is valuable
- **Module Info** — Which BMAD module it belongs to

### Workflow Conventions

- Use frontmatter in all `.md` files
- Include `MANDATORY EXECUTION RULES` in every step
- Include `SYSTEM SUCCESS/FAILURE METRICS` in every step
- End every step with a menu that halts execution
- Track progress in `stepsCompleted` frontmatter
- Use `{variable}` syntax for config values (not hardcoded paths)
- Include subprocess fallback instructions

### Quality Checklist

Before submitting, verify:

- [ ] All step files follow the standard structure
- [ ] Variables are used instead of hardcoded values
- [ ] Every step has clear success/failure metrics
- [ ] Menus halt execution and wait for user input
- [ ] The workflow is resumable (step-01b handles continuation)
- [ ] README is complete and clear
- [ ] No project-specific content remains

## How to Submit

### 1. Fork This Repository

Fork this repo and create a branch for your workflow.

### 2. Add Your Workflow

Place your workflow folder inside `workflows/`:

```
workflows/
├── dev-checkpoint/    # Existing
└── your-workflow/     # New
```

### 3. Update the Main README

Add your workflow to the table in the root `README.md`:

```markdown
| [your-workflow](workflows/your-workflow/) | Description | Use when... |
```

### 4. Open a Pull Request

Include in your PR description:

- What problem the workflow solves
- How you've tested it
- Which BMAD module it targets

## Style Guide

### Naming

- Workflow folder: `kebab-case` (e.g., `dev-checkpoint`, `sprint-review`)
- Step files: `step-XX-name.md` (e.g., `step-01-init.md`, `step-02-analysis.md`)
- Output files: `descriptive-name.md` (e.g., `codebase-analysis.md`)

### Language

- Workflow instructions can be in any language
- README should be in English (with additional languages welcome)
- Use `{communication_language}` variable for runtime language switching

### Tone

- Step instructions: Direct, imperative ("Scan the project", "Present findings")
- READMEs: Clear, friendly, no unnecessary jargon
- Error metrics: Specific ("Not reading the complete file" not "Doing it wrong")

## Questions?

Open an issue if you have questions about contributing or need help structuring your workflow.

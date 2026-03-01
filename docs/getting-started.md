# Getting Started

This guide walks you through installing and using a custom BMAD workflow in your project.

## Prerequisites

Before you begin, make sure you have:

- **A BMAD-enabled project** — Your project should have a `_bmad/` folder with the BMAD Method set up (v6+)
- **An AI IDE** — Claude Code, Cursor, Windsurf, or any IDE that supports BMAD agents
- **A `config.yaml`** — Your BMAD module should have a config file with project settings

If you don't have BMAD set up yet, visit the [BMAD Method repository](https://github.com/bmadcode/BMAD-METHOD) to get started.

## Installation

### Step 1: Choose a Workflow

Browse the [workflows/](../workflows/) folder and pick the workflow you want. Each workflow has its own README with details about what it does.

### Step 2: Identify the Target Module

BMAD workflows belong to specific modules. Check the workflow's README to find which module it belongs to:

| Module | Path | Description |
|--------|------|-------------|
| BMM | `_bmad/bmm/workflows/` | Software development (planning, building, shipping) |
| Core | `_bmad/core/workflows/` | Cross-module utilities |
| CIS | `_bmad/cis/workflows/` | Creative and innovation |
| TEA | `_bmad/tea/workflows/` | Testing and quality |

### Step 3: Copy the Workflow

Copy the entire workflow folder into the correct location in your project:

```bash
# Example: dev-checkpoint belongs to BMM, phase 4 (implementation)
cp -r workflows/dev-checkpoint/ your-project/_bmad/bmm/workflows/4-implementation/dev-checkpoint/
```

> Keep the folder name as-is. BMAD uses folder names for workflow identification.

### Step 4: Register the Workflow (if needed)

Some BMAD setups auto-discover workflows. If yours doesn't, you may need to register it in your module's manifest or config file.

Check your `_bmad/bmm/manifest.yaml` (or equivalent) to see if workflows need explicit registration.

### Step 5: Launch

Use your AI IDE's BMAD command system:

```
/bmad-bmm-dev-checkpoint
```

Or simply ask your AI assistant in natural language:

```
"Run the dev checkpoint workflow"
"Do a dev checkpoint"
"Faire un point de dev"
```

## What to Expect

When a workflow runs:

1. **Initialization** — The workflow loads, detects your project context, and asks a few questions
2. **Autonomous phases** — The AI analyzes your code and/or artifacts (no input needed)
3. **Collaborative phases** — The AI presents findings and asks for your decisions
4. **Application** — Changes are applied based on your decisions
5. **Summary** — A final report is generated

Progress is tracked, so if your session ends mid-workflow, you can resume where you left off.

## Troubleshooting

### "Workflow not found"

- Verify the workflow folder is in the correct module directory
- Check that your BMAD manifest includes the workflow
- Ensure the folder name matches exactly

### "Config variables not resolved"

- Make sure your `_bmad/{module}/config.yaml` contains the required variables
- Common variables: `project_name`, `output_folder`, `user_name`, `communication_language`

### Session ended mid-workflow

- Re-launch the same workflow command
- It will detect the in-progress checkpoint and offer to resume

## Next Steps

- Read [workflow-anatomy.md](workflow-anatomy.md) to understand how workflows are structured
- Explore specific workflow READMEs for detailed usage instructions

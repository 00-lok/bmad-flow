# BMAD Custom Workflows

> A curated collection of custom workflows for the [BMAD Method](https://github.com/bmadcode/BMAD-METHOD) — ready to drop into any BMAD-powered project.

## What is BMAD?

**BMAD** (BMad Agentic Development) is a methodology for AI-assisted software development. It uses structured agents, workflows, and artifacts to guide projects from ideation to deployment. Workflows are step-by-step processes that AI agents follow to accomplish specific tasks.

**This repository** contains custom workflows that extend the standard BMAD toolkit with specialized capabilities.

## Available Workflows

| Workflow | Description | Use When |
|----------|-------------|----------|
| [dev-checkpoint](workflows/dev-checkpoint/) | Reconcile BMAD artifacts with code reality | Your planning docs have drifted from your actual codebase |

## Quick Start

### 1. Prerequisites

- A project using the [BMAD Method](https://github.com/bmadcode/BMAD-METHOD) (v6+)
- An AI-powered IDE (Claude Code, Cursor, Windsurf, etc.)
- An existing `_bmad/` folder in your project

### 2. Install a Workflow

Copy the workflow folder into your project's BMAD module directory:

```bash
# Example: install dev-checkpoint into the BMM module
cp -r workflows/dev-checkpoint/ your-project/_bmad/bmm/workflows/4-implementation/dev-checkpoint/
```

### 3. Use It

Launch the workflow from your AI IDE using the BMAD command system:

```
/bmad-bmm-dev-checkpoint
```

Or ask your AI assistant:

```
"Run the dev checkpoint workflow"
```

> For detailed installation instructions, see [docs/getting-started.md](docs/getting-started.md).

## Repository Structure

```
BMAD_Customs_Workflows/
├── README.md                  # You are here
├── CONTRIBUTING.md            # How to contribute your own workflows
├── LICENSE                    # MIT License
├── docs/
│   ├── getting-started.md     # Installation & first use guide
│   └── workflow-anatomy.md    # Understanding BMAD workflow architecture
└── workflows/
    └── dev-checkpoint/        # Each workflow in its own folder
        ├── README.md          # Workflow documentation
        ├── workflow.md        # Workflow definition (entry point)
        ├── workflow-plan.md   # Design document (for transparency)
        ├── data/              # Templates and data files
        └── steps-c/           # Step files (executed sequentially)
```

## How Workflows Work

Each workflow follows the **BMAD micro-file architecture**:

1. **`workflow.md`** is the entry point — it defines the goal, role, and rules
2. **Step files** in `steps-c/` are loaded one at a time (just-in-time loading)
3. Steps execute sequentially — no skipping or reordering
4. Progress is tracked in output file frontmatter
5. Menus at the end of each step let you control the pace

> For a deeper understanding, see [docs/workflow-anatomy.md](docs/workflow-anatomy.md).

## Contributing

We welcome contributions! If you've built a useful BMAD workflow, consider sharing it.

See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

This project is licensed under the MIT License — see [LICENSE](LICENSE) for details.

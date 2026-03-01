# Guide d'Intégration

Ce guide vous accompagne dans l'installation complète d'un workflow BMAD personnalisé dans votre projet — de la copie des fichiers jusqu'à la commande fonctionnelle dans votre IDE.

## Prérequis

- **Un projet BMAD** — Votre projet doit avoir un dossier `_bmad/` avec la BMAD Method configurée (v6+)
- **Un IDE IA** — Claude Code, Cursor, Windsurf, ou tout IDE supportant les agents BMAD
- **Un `config.yaml`** — Votre module BMAD doit avoir un fichier de configuration avec les paramètres du projet

Si vous n'avez pas encore BMAD, visitez le [dépôt BMAD Method](https://github.com/bmadcode/BMAD-METHOD) pour commencer.

---

## Installation en 4 étapes

### Étape 1 : Copier le workflow

Chaque workflow a un **module cible** (indiqué dans son README). Copiez le dossier complet dans le bon emplacement de votre projet :

| Module | Chemin de destination | Description |
|--------|----------------------|-------------|
| Core | `_bmad/core/workflows/` | Utilitaires transversaux |
| BMM | `_bmad/bmm/workflows/{phase}/` | Développement logiciel |
| CIS | `_bmad/cis/workflows/` | Créativité et innovation |
| TEA | `_bmad/tea/workflows/` | Tests et qualité |

```bash
# Exemple : smart-commit (module Core)
cp -r workflows/smart-commit/ votre-projet/_bmad/core/workflows/smart-commit/

# Exemple : dev-checkpoint (module BMM, phase 4)
cp -r workflows/dev-checkpoint/ votre-projet/_bmad/bmm/workflows/4-implementation/dev-checkpoint/
```

> Gardez le nom du dossier tel quel. BMAD utilise les noms de dossiers pour l'identification des workflows.

---

### Étape 2 : Enregistrer dans le manifeste

Ajoutez une ligne au fichier `_bmad/_config/workflow-manifest.csv` de votre projet pour que BMAD reconnaisse le workflow.

**Format du manifeste :**

```csv
name,description,module,path
```

| Champ | Description | Exemple |
|-------|-------------|---------|
| `name` | Identifiant unique du workflow (kebab-case) | `"smart-commit"` |
| `description` | Description + déclencheurs en langage naturel | `"Analyse les changements... Use when user says smart commit"` |
| `module` | Module BMAD (`core`, `bmm`, `cis`, `tea`) | `"core"` |
| `path` | Chemin relatif vers le `workflow.md` depuis la racine du projet | `"_bmad/core/workflows/smart-commit/workflow.md"` |

**Comment faire :** Ouvrez `_bmad/_config/workflow-manifest.csv` et ajoutez une nouvelle ligne à la fin. Chaque workflow de ce dépôt fournit la ligne exacte à copier dans son README.

---

### Étape 3 : Créer la commande IDE

Pour que la commande `/bmad-nom-du-workflow` apparaisse dans votre IDE, vous devez créer un fichier de commande dans le dossier approprié. Le format varie selon l'IDE.

#### Cursor / Claude Code / Augment

**Dossier :** `.cursor/commands/`, `.claude/commands/`, ou `.augment/commands/`
**Fichier :** `bmad-nom-du-workflow.md`

```markdown
---
name: 'nom-du-workflow'
description: 'Description du workflow...'
---

IT IS CRITICAL THAT YOU FOLLOW THIS COMMAND: LOAD the FULL {project-root}/_bmad/MODULE/workflows/NOM/workflow.md, READ its entire contents and follow its directions exactly!
```

#### Clinerules

**Dossier :** `.clinerules/workflows/`
**Fichier :** `bmad-nom-du-workflow.md`

```markdown
---
description: 'Description du workflow...'
auto_execution_mode: "iterate"
---

# nom-du-workflow

Read the entire workflow file at {project-root}/_bmad/MODULE/workflows/NOM/workflow.md

Follow all instructions in the workflow file exactly as written.
```

#### Gemini

**Dossier :** `.gemini/commands/`
**Fichier :** `bmad-nom-du-workflow.toml`

```toml
description = "Description du workflow..."
prompt = """
Execute the BMAD 'nom-du-workflow' workflow.

CRITICAL: You must load and follow the workflow definition exactly.

WORKFLOW INSTRUCTIONS:
1. LOAD the workflow file from {project-root}/_bmad/MODULE/workflows/NOM/workflow.md
2. READ its entire contents
3. FOLLOW every step precisely as specified
4. DO NOT skip or modify any steps

WORKFLOW FILE: {project-root}/_bmad/MODULE/workflows/NOM/workflow.md
"""
```

#### GitHub Copilot

**Dossier :** `.github/prompts/`
**Fichier :** `bmad-nom-du-workflow.prompt.md`

```markdown
---
description: 'Description courte du workflow'
agent: 'agent'
tools: ['read', 'edit', 'search', 'execute']
---

1. Load {project-root}/_bmad/core/config.yaml and store ALL fields as session variables
2. Load and follow the workflow at {project-root}/_bmad/MODULE/workflows/NOM/workflow.md
```

> Chaque workflow de ce dépôt fournit les templates pré-remplis dans son README — il suffit de copier-coller.

---

### Étape 4 : Vérifier et lancer

1. **Vérifiez** que le dossier du workflow est au bon emplacement dans `_bmad/`
2. **Vérifiez** que la ligne a été ajoutée au manifeste CSV
3. **Ouvrez un nouveau chat** dans votre IDE (les commandes ne sont pas rechargées en cours de session)
4. **Tapez** `/bmad-nom-du-workflow` — la commande devrait apparaître

Vous pouvez aussi lancer le workflow en langage naturel :

```
"Fais un smart commit"
"Lance le dev checkpoint"
```

---

## À Quoi S'Attendre

Quand un workflow s'exécute :

1. **Initialisation** — Le workflow se charge, détecte le contexte de votre projet et pose quelques questions
2. **Phases autonomes** — L'IA analyse votre code et/ou vos artefacts (pas d'entrée nécessaire)
3. **Phases collaboratives** — L'IA présente ses résultats et demande vos décisions
4. **Application** — Les changements sont appliqués selon vos décisions
5. **Résumé** — Un rapport final est généré

La progression est suivie, donc si votre session se termine en cours de workflow, vous pouvez reprendre là où vous en étiez.

---

## Dépannage

### La commande `/bmad-xxx` n'apparaît pas

- Vérifiez que le fichier de commande existe dans le bon dossier IDE (`.cursor/commands/`, `.claude/commands/`, etc.)
- Vérifiez que le nom du fichier suit le pattern `bmad-nom-du-workflow.md`
- **Ouvrez un nouveau chat** — les commandes ne sont pas rechargées dans un chat existant

### "Workflow not found" ou fichier introuvable

- Vérifiez que le dossier du workflow est dans le bon répertoire de module
- Vérifiez que le chemin dans la commande IDE correspond au chemin réel du `workflow.md`
- Vérifiez que le manifeste CSV contient le bon chemin

### "Variables de configuration non résolues"

- Assurez-vous que votre `_bmad/{module}/config.yaml` contient les variables requises
- Variables courantes : `project_name`, `output_folder`, `user_name`, `communication_language`

### Session terminée en cours de workflow

- Relancez la même commande de workflow
- Il détectera le checkpoint en cours et proposera de reprendre (si le workflow est continuable)

---

## Prochaines Étapes

- Lisez [workflow-anatomy.md](workflow-anatomy.md) pour comprendre comment les workflows sont structurés
- Explorez les READMEs spécifiques des workflows pour des instructions d'utilisation détaillées

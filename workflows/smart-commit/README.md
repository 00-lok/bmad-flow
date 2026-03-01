# Smart Commit

Workflow BMAD qui analyse intelligemment le contexte d'un projet et tous les changements non commités pour générer un plan de commits optimal, puis exécute les commits après validation.

## Objectif

Transformer un ensemble de changements non commités en une série de commits propres, atomiques et bien nommés — automatiquement. Le workflow détecte les conventions du projet, comprend les relations entre fichiers, et propose un plan de commits logique qui respecte les bonnes pratiques git.

## Fonctionnement

Le workflow s'exécute en 5 étapes :

| Étape | Mode | Description |
|-------|------|-------------|
| **1. Init** | Auto | Vérifie le dépôt git et la présence de changements |
| **2. Contexte** | Autonome | Analyse la structure du projet et les conventions de commit |
| **3. Changements** | Autonome | Analyse en détail chaque changement, catégorise et groupe |
| **4. Plan** | Collaboratif | Présente le plan de commits pour validation |
| **5. Exécution** | Autonome | Crée les commits selon le plan validé |

**Seule interaction requise :** valider (ou ajuster) le plan de commits à l'étape 4.

## Caractéristiques

- **Détection automatique des conventions** : Conventional Commits, Gitmoji, préfixes custom, ou patterns spécifiques au projet
- **Commits atomiques** : un concern logique par commit
- **Ordre intelligent** : infrastructure → dépendances → modèles → code partagé → features → tests → docs
- **Messages conformes** : respecte la langue et le format détectés dans l'historique
- **Sécurité** : aucun push automatique, arrêt immédiat en cas d'erreur, pas de flags destructifs
- **Réutilisable** : fonctionne dans tout projet git avec BMAD installé

## Installation

### Infos module

- **Module cible :** Core (standalone)
- **Type :** Single-session, non-document, create-only
- **Config requise :** `_bmad/core/config.yaml` (`user_name`, `communication_language`)

### 1. Copier le workflow

```bash
cp -r workflows/smart-commit/ votre-projet/_bmad/core/workflows/smart-commit/
```

### 2. Ajouter au manifeste

Ajoutez cette ligne à la fin de `_bmad/_config/workflow-manifest.csv` dans votre projet :

```csv
"smart-commit","Analyse le contexte projet et les changements non commités pour créer un plan de commits intelligent. Utiliser quand l'utilisateur dit ""smart commit"" ou ""commiter intelligemment"" ou ""prépare mes commits""","core","_bmad/core/workflows/smart-commit/workflow.md"
```

### 3. Créer la commande IDE

Créez le fichier de commande correspondant à votre IDE :

#### Cursor

Créez `.cursor/commands/bmad-smart-commit.md` :

```markdown
---
name: 'smart-commit'
description: 'Analyse le contexte projet et les changements non commités pour créer un plan de commits intelligent.'
---

IT IS CRITICAL THAT YOU FOLLOW THIS COMMAND: LOAD the FULL {project-root}/_bmad/core/workflows/smart-commit/workflow.md, READ its entire contents and follow its directions exactly!
```

#### Claude Code

Créez `.claude/commands/bmad-smart-commit.md` :

```markdown
---
name: 'smart-commit'
description: 'Analyse le contexte projet et les changements non commités pour créer un plan de commits intelligent.'
---

IT IS CRITICAL THAT YOU FOLLOW THIS COMMAND: LOAD the FULL {project-root}/_bmad/core/workflows/smart-commit/workflow.md, READ its entire contents and follow its directions exactly!
```

#### Gemini

Créez `.gemini/commands/bmad-smart-commit.toml` :

```toml
description = "Analyse le contexte projet et les changements non commités pour créer un plan de commits intelligent."
prompt = """
Execute the BMAD 'smart-commit' workflow.

CRITICAL: You must load and follow the workflow definition exactly.

WORKFLOW INSTRUCTIONS:
1. LOAD the workflow file from {project-root}/_bmad/core/workflows/smart-commit/workflow.md
2. READ its entire contents
3. FOLLOW every step precisely as specified
4. DO NOT skip or modify any steps

WORKFLOW FILE: {project-root}/_bmad/core/workflows/smart-commit/workflow.md
"""
```

#### GitHub Copilot

Créez `.github/prompts/bmad-smart-commit.prompt.md` :

```markdown
---
description: 'Smart commit — plan de commits intelligent'
agent: 'agent'
tools: ['read', 'edit', 'search', 'execute']
---

1. Load {project-root}/_bmad/core/config.yaml and store ALL fields as session variables
2. Load and follow the workflow at {project-root}/_bmad/core/workflows/smart-commit/workflow.md
```

### 4. Vérifier

Ouvrez un **nouveau chat** dans votre IDE et tapez `/bmad-smart-commit` — la commande devrait apparaître.

## Utilisation

### Via commande BMAD

```
/bmad-smart-commit
```

### En langage naturel

```
"Fais un smart commit"
"Prépare mes commits intelligemment"
"Analyse et commite mes changements"
```

## Exemple de résultat

Pour un projet avec 12 fichiers modifiés :

```
📋 Plan de commits — 4 commit(s) proposés

━━━ Commit 1/4 ━━━
Message: chore(deps): update package-lock.json
Fichiers (1): package-lock.json

━━━ Commit 2/4 ━━━
Message: feat(auth): add JWT token refresh mechanism
Fichiers (4): src/auth/token.ts, src/auth/refresh.ts, src/auth/types.ts, src/middleware/auth.ts

━━━ Commit 3/4 ━━━
Message: test(auth): add token refresh unit tests
Fichiers (3): tests/auth/token.test.ts, tests/auth/refresh.test.ts, tests/fixtures/auth.ts

━━━ Commit 4/4 ━━━
Message: docs(auth): document token refresh flow
Fichiers (2): docs/auth.md, README.md
```

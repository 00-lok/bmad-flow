# Dev Checkpoint

> Faites le point sur l'état réel de votre développement, identifiez les écarts entre vos plans et votre code, et réalignez vos artefacts BMAD pour qu'ils redeviennent une source de vérité fiable.

## Le Problème

Au fil du développement, la réalité du code s'éloigne naturellement de ce qui a été planifié. Des fonctionnalités sont ajoutées ou modifiées sans mise à jour de la documentation. Des décisions d'architecture prises en cours de route ne sont jamais reflétées dans les artefacts. Le PRD décrit des choses qui n'existent plus, et des stories sont implémentées différemment de ce qui était prévu.

Résultat : votre IA de développement travaille avec un contexte obsolète. Elle prend des décisions basées sur une vision du projet qui ne correspond plus à la réalité — ce qui dégrade la qualité de l'assistance et génère des erreurs évitables.

## Ce Que Fait Ce Workflow

**Dev Checkpoint** réalise un état des lieux complet de votre projet en 7 étapes — il analyse le code, lit chaque artefact BMAD, identifie toutes les divergences, vous aide à prendre des décisions de réalignement, puis met à jour vos documents automatiquement :

| Étape | Mode | Description |
|-------|------|-------------|
| **1. Init** | Semi-collaboratif | Détecter les artefacts, recueillir le contexte, créer le dossier checkpoint |
| **1b. Continue** | Auto | Reprendre une session précédente (si interrompue) |
| **2. Code** | Autonome | Analyse approfondie de l'intégralité du codebase |
| **3. Artefacts** | Autonome | Lecture et évaluation de chaque artefact BMAD |
| **4. Diagnostic** | Autonome | Comparaison code vs. artefacts — identification des désalignements |
| **5. Décisions** | Collaboratif | Décider ensemble : mettre à jour les docs OU corriger le code |
| **6. Application** | Autonome | Appliquer les mises à jour aux artefacts + compiler les actions code |
| **7. Snapshot** | Autonome | Générer un résumé de santé du projet |

### Ce Que Vous Obtenez

Un dossier checkpoint horodaté contenant :

| Fichier | Description |
|---------|-------------|
| `checkpoint-summary.md` | Vue d'ensemble du projet avec score de santé |
| `codebase-analysis.md` | Revue complète du code (structure, qualité, dette technique) |
| `artifacts-review.md` | Revue de chaque artefact BMAD |
| `misalignment-report.md` | Chaque divergence entre le plan et la réalité |
| `decisions-log.md` | Vos décisions sur la gestion de chaque divergence |
| `action-items.md` | Liste priorisée des corrections code à planifier |

En plus : **vos artefacts BMAD sont mis à jour sur place** pour refléter la réalité.

## Installation

### Infos module

- **Module cible :** BMM (Software Development)
- **Phase :** 4-implementation
- **Type de session :** Continuable (reprise possible)
- **Config requise :** `_bmad/bmm/config.yaml` (`project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`, `planning_artifacts`)

### 1. Copier le workflow

```bash
cp -r workflows/incubation/dev-checkpoint/ votre-projet/_bmad/bmm/workflows/4-implementation/dev-checkpoint/
```

### 2. Ajouter au manifeste

Ajoutez cette ligne à la fin de `_bmad/_config/workflow-manifest.csv` dans votre projet :

```csv
"dev-checkpoint","État des lieux complet du développement — analyse le code et les artefacts BMAD, identifie les divergences et réaligne la documentation. Utiliser quand l'utilisateur dit ""dev checkpoint"" ou ""faire un point de dev"" ou ""état des lieux du projet""","bmm","_bmad/bmm/workflows/4-implementation/dev-checkpoint/workflow.md"
```

### 3. Créer la commande IDE

Créez le fichier de commande correspondant à votre IDE :

#### Cursor

Créez `.cursor/commands/bmad-bmm-dev-checkpoint.md` :

```markdown
---
name: 'dev-checkpoint'
description: 'État des lieux du développement — analyse code et artefacts BMAD, identifie les divergences et réaligne la documentation.'
---

IT IS CRITICAL THAT YOU FOLLOW THIS COMMAND: LOAD the FULL {project-root}/_bmad/bmm/workflows/4-implementation/dev-checkpoint/workflow.md, READ its entire contents and follow its directions exactly!
```

#### Claude Code

Créez `.claude/commands/bmad-bmm-dev-checkpoint.md` :

```markdown
---
name: 'dev-checkpoint'
description: 'État des lieux du développement — analyse code et artefacts BMAD, identifie les divergences et réaligne la documentation.'
---

IT IS CRITICAL THAT YOU FOLLOW THIS COMMAND: LOAD the FULL {project-root}/_bmad/bmm/workflows/4-implementation/dev-checkpoint/workflow.md, READ its entire contents and follow its directions exactly!
```

#### Gemini

Créez `.gemini/commands/bmad-bmm-dev-checkpoint.toml` :

```toml
description = "État des lieux du développement — analyse code et artefacts BMAD, identifie les divergences et réaligne la documentation."
prompt = """
Execute the BMAD 'dev-checkpoint' workflow.

CRITICAL: You must load and follow the workflow definition exactly.

WORKFLOW INSTRUCTIONS:
1. LOAD the workflow file from {project-root}/_bmad/bmm/workflows/4-implementation/dev-checkpoint/workflow.md
2. READ its entire contents
3. FOLLOW every step precisely as specified
4. DO NOT skip or modify any steps

WORKFLOW FILE: {project-root}/_bmad/bmm/workflows/4-implementation/dev-checkpoint/workflow.md
"""
```

#### GitHub Copilot

Créez `.github/prompts/bmad-bmm-dev-checkpoint.prompt.md` :

```markdown
---
description: 'Dev checkpoint — état des lieux dev et réalignement artefacts BMAD'
agent: 'agent'
tools: ['read', 'edit', 'search', 'execute']
---

1. Load {project-root}/_bmad/bmm/config.yaml and store ALL fields as session variables
2. Load and follow the workflow at {project-root}/_bmad/bmm/workflows/4-implementation/dev-checkpoint/workflow.md
```

### 4. Vérifier la config

Votre `_bmad/bmm/config.yaml` doit inclure ces variables :

```yaml
project_name: "Votre Projet"
output_folder: "_bmad-output"
user_name: "Votre Nom"
communication_language: "french"
document_output_language: "french"
```

### 5. Lancer

Ouvrez un **nouveau chat** et tapez :

```
/bmad-bmm-dev-checkpoint
```

Ou en langage naturel :

```
"Fais un point de dev"
"Lance le dev checkpoint"
"Réconcilie les artefacts avec le code"
```

## Fonctionnement détaillé

### Phase 1 : Initialisation (Étape 1)

Le workflow :
- Scanne votre projet pour les artefacts BMAD existants (PRD, architecture, stories, etc.)
- Vous pose 2-3 questions ciblées sur les changements récents
- Crée un dossier checkpoint horodaté

### Phase 2 : Analyse (Étapes 2-3) — Autonome

L'IA effectue une analyse approfondie sans intervention de votre part :
- **Étape 2** : Scanne l'intégralité de votre codebase — structure, qualité du code, dépendances, historique git, dette technique
- **Étape 3** : Lit et évalue chaque artefact BMAD — complétude, clarté, cohérence interne

### Phase 3 : Diagnostic (Étape 4) — Autonome

L'IA croise code et artefacts pour identifier chaque désalignement, catégorisé par :
- **Architecture** — Divergences structurelles
- **Fonctionnel** — Lacunes de couverture des fonctionnalités
- **UX/UI** — Divergences de design
- **Tech/Stack** — Différences de choix techniques
- **Documentation** — Artefacts incomplets ou obsolètes

Chaque désalignement est noté : rouge (critique), jaune (important), vert (mineur).

### Phase 4 : Décisions (Étape 5) — Collaboratif

Pour chaque désalignement, vous choisissez :
- **[D] Mettre à jour la documentation** — Le code est correct, mettre à jour l'artefact
- **[C] Action code** — Le doc est correct, noter une correction pour le code

### Phase 5 : Application (Étape 6) — Autonome

L'IA met à jour vos artefacts BMAD sur place, vérifie la cohérence inter-artefacts, et compile les actions code en liste priorisée.

### Phase 6 : Snapshot (Étape 7) — Autonome

Un résumé lisible est généré avec score de santé, vue d'ensemble, réalignements effectués, actions restantes et priorités recommandées.

## Reprise

Le workflow suit la progression via `stepsCompleted` dans le frontmatter du checkpoint. Si votre session s'interrompt :

1. Relancez le workflow
2. Il détecte le checkpoint en cours
3. Reprend automatiquement à l'étape suivante

## Quand l'utiliser

- Après une phase de développement significative
- Quand vous sentez que vos docs de planification sont obsolètes
- Avant de démarrer un nouveau sprint ou un nouvel ensemble de fonctionnalités
- Lors de l'onboarding pour comprendre l'état du projet
- Périodiquement (toutes les 2-4 semaines de développement actif)

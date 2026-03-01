# Comprendre l'Architecture des Workflows BMAD

Ce document explique comment les workflows BMAD sont structurés pour que vous puissiez les comprendre, les modifier ou créer les vôtres.

## Concepts Fondamentaux

### Architecture Micro-Fichiers

Les workflows BMAD utilisent un **design micro-fichiers** où chaque étape est un fichier d'instruction autonome. Cela signifie :

- L'IA ne charge qu'**une étape à la fois** (chargement juste-à-temps)
- Chaque fichier d'étape contient tout le nécessaire pour exécuter cette étape
- Les étapes s'exécutent dans un ordre strict — pas de saut ni de réordonnancement
- La progression est suivie dans le frontmatter des fichiers de sortie

### Pourquoi les Micro-Fichiers ?

1. **Efficacité du contexte** — Les modèles IA ont des fenêtres de contexte limitées. Charger une étape à la fois garde le contexte concentré
2. **Reprise possible** — Si une session se termine, le workflow peut reprendre à la dernière étape complétée
3. **Clarté** — Chaque étape a un objectif clair et délimité
4. **Maintenabilité** — Les étapes peuvent être mises à jour indépendamment

## Structure des Fichiers

Chaque workflow BMAD suit cette structure :

```
nom-du-workflow/
├── workflow.md              # Point d'entrée — définit l'objectif, le rôle et les règles
├── workflow-plan.md         # Document de conception (optionnel, pour la transparence)
├── data/                    # Templates, schémas, données de référence
│   └── template.md
└── steps-c/                 # Fichiers d'étapes (c = mode création)
    ├── step-01-init.md      # Commence toujours par l'initialisation
    ├── step-01b-continue.md # Gestionnaire de continuation (pour les workflows reprenables)
    ├── step-02-*.md         # Étapes suivantes
    ├── step-03-*.md
    └── ...
```

### Nommage des Dossiers : `steps-c/`, `steps-u/`, `steps-d/`

BMAD supporte trois modes de cycle de vie :

| Dossier | Mode | Description |
|---------|------|-------------|
| `steps-c/` | **Création** | Étapes pour créer quelque chose de nouveau |
| `steps-u/` | **Mise à jour** | Étapes pour modifier un travail existant |
| `steps-d/` | **Suppression** | Étapes pour supprimer ou archiver |

La plupart des workflows n'utilisent que `steps-c/`. Les workflows tri-modaux incluent les trois.

## Anatomie de `workflow.md`

Le fichier point d'entrée contient :

```markdown
---
name: Nom du Workflow
description: Ce que fait ce workflow
web_bundle: true
---

# Nom du Workflow

**Objectif :** [Énoncé clair de ce que le workflow accomplit]

**Votre Rôle :** [Comment l'IA doit se comporter pendant ce workflow]

## ARCHITECTURE DU WORKFLOW
[Principes fondamentaux et règles]

## SÉQUENCE D'INITIALISATION
[Comment démarrer — charger la config, exécuter la première étape]
```

### Sections Clés

- **Objectif** — Ce que le workflow produit et pourquoi
- **Votre Rôle** — Persona et expertise que l'IA adopte
- **Principes Fondamentaux** — Règles que l'IA doit suivre (design micro-fichiers, exécution séquentielle, etc.)
- **Règles Critiques** — Contraintes non négociables (ne jamais charger plusieurs étapes, toujours attendre l'entrée utilisateur aux menus, etc.)
- **Séquence d'Initialisation** — Chargement de la config et exécution de la première étape

## Anatomie d'un Fichier d'Étape

Chaque fichier d'étape suit une structure cohérente :

```markdown
---
name: 'step-XX-nom'
description: 'Ce que fait cette étape'
nextStepFile: './step-XX+1-nom.md'
checkpointFolder: '{checkpointFolder}'
---

# Étape X : Titre

## OBJECTIF DE L'ÉTAPE :
[Énoncé clair de l'objectif de cette étape]

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE D'ABORD) :
### Règles Universelles :    [Règles applicables à toutes les étapes]
### Rappel du Rôle :         [Rappels de la persona]
### Règles Spécifiques :     [Règles uniques à cette étape]

## PROTOCOLES D'EXÉCUTION :
[Comment exécuter cette étape]

## LIMITES DU CONTEXTE :
[Quelles informations sont disponibles et lesquelles sont hors limites]

## SÉQUENCE OBLIGATOIRE
[Séquence numérotée d'actions — à suivre exactement]

### 1. [Première Action]
### 2. [Deuxième Action]
...

### N. Présenter les OPTIONS DU MENU
Afficher : **[C] Continuer — [description]**

## MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME
### SUCCÈS : [Ce qui constitue un succès]
### ÉCHEC : [Ce qui constitue un échec]
```

### Éléments Clés

| Élément | Utilité |
|---------|---------|
| **Frontmatter** | Métadonnées : nom, description, chemin de l'étape suivante, variables |
| **Objectif de l'Étape** | Un seul objectif clair pour cette étape |
| **Règles d'Exécution** | Contraintes que l'IA doit respecter |
| **Limites du Contexte** | Quelles données sont disponibles vs. interdites |
| **Séquence Obligatoire** | Actions exactes dans l'ordre — le cœur de l'étape |
| **Menu** | Point de contrôle utilisateur — le workflow s'arrête ici |
| **Métriques de Succès/Échec** | Comment évaluer si l'étape a été correctement exécutée |

## Gestion de l'État

Les workflows suivent la progression via le **frontmatter dans les fichiers de sortie** :

```yaml
---
stepsCompleted: ['step-01-init', 'step-02-analysis']
lastStep: 'step-02-analysis'
status: IN_PROGRESS
---
```

- `stepsCompleted` — Tableau des noms d'étapes complétées
- `lastStep` — Dernière étape complétée
- `status` — `IN_PROGRESS` ou `COMPLETE`

Cela permet la **reprise de session** : si le workflow est interrompu, `step-01b-continue.md` lit le frontmatter et route vers l'étape suivante.

## Résolution des Variables

Les fichiers d'étapes utilisent des variables résolues depuis la config BMAD :

| Variable | Source | Exemple |
|----------|--------|---------|
| `{project-root}` | Détection automatique | `/home/user/mon-projet` |
| `{project_name}` | `config.yaml` | `Mon App` |
| `{output_folder}` | `config.yaml` | `_bmad-output` |
| `{user_name}` | `config.yaml` | `Doens` |
| `{communication_language}` | `config.yaml` | `french` |
| `{checkpointFolder}` | Défini pendant step-01 | `_bmad-output/dev-checkpoints/2026-02-28T14-30-00` |

## Système de Menus

Chaque étape se termine par un menu qui interrompt l'exécution :

```markdown
### Présenter les OPTIONS DU MENU

Afficher : **[C] Continuer — Lancer l'analyse**

#### Logique de Gestion du Menu :
- SI C : vérifier les sorties, charger et exécuter l'étape suivante
- SI Autre : aider l'utilisateur, réafficher le menu
```

L'IA **doit s'arrêter et attendre l'entrée utilisateur** aux menus. Cela vous donne le contrôle du rythme.

Options de menu courantes :

| Option | Signification |
|--------|---------------|
| `[C]` | Continuer vers l'étape suivante |
| `[A]` | Élicitation avancée (exploration plus poussée) |
| `[P]` | Party mode (brainstorming créatif) |

## Optimisation des Subprocess

Certaines étapes peuvent exploiter les **sub-agents** pour le traitement parallèle :

```markdown
- Pattern Subprocess 2 : Un sub-agent par élément (ex. un par artefact)
- Pattern Subprocess 4 : Comparaisons parallèles par catégorie
- Fallback : Traitement séquentiel dans le thread principal
```

Si l'IA n'a pas de capacités de sub-agents, elle revient au traitement séquentiel. Le workflow gère cela gracieusement.

## Créer Votre Propre Workflow

Voir [CONTRIBUTING.md](../CONTRIBUTING.md) pour les directives de création et de soumission de nouveaux workflows.

Principes clés :

1. **Un objectif par workflow** — Restez concentré
2. **Étapes micro-fichiers** — Un concern par fichier d'étape
3. **Limites claires** — Chaque étape sait ce qu'elle peut et ne peut pas faire
4. **Contrôle utilisateur** — Menus à chaque point de transition
5. **Suivi d'état** — Permettre la reprise
6. **Fallbacks gracieux** — Fonctionner avec ou sans sub-agents

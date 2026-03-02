# BMAD Custom Workflows

> Une collection de workflows personnalisés pour la [BMAD Method](https://github.com/bmadcode/BMAD-METHOD) — prêts à être intégrés dans n'importe quel projet BMAD.

## Qu'est-ce que BMAD ?

**BMAD** (BMad Agentic Development) est une méthodologie pour le développement logiciel assisté par IA. Elle utilise des agents structurés, des workflows et des artefacts pour guider les projets de l'idéation au déploiement. Les workflows sont des processus étape par étape que les agents IA suivent pour accomplir des tâches spécifiques.

**Ce dépôt** contient des workflows personnalisés qui étendent la boîte à outils BMAD standard avec des capacités spécialisées.

## Workflows Disponibles

| Workflow | Module | Description | Quand l'utiliser |
|----------|--------|-------------|------------------|
| [dev-checkpoint](workflows/incubation/dev-checkpoint/) | BMM | État des lieux complet du développement : analyse le code et les artefacts BMAD, identifie les divergences, et réaligne la documentation avec la réalité du projet | Après une phase de dev significative, quand vos docs de planification ne reflètent plus le code réel |
| [smart-commit](workflows/incubation/smart-commit/) | Core | Analyser et commiter intelligemment les changements | Vous avez des changements à commiter proprement |

Les deux workflows actuels sont en `workflows/incubation/` (statut expérimental / en cours de test).

## Intégration en 4 Étapes

Pour intégrer un workflow dans votre projet BMAD :

1. **Copier** le dossier du workflow dans `_bmad/{module}/workflows/` de votre projet
2. **Enregistrer** le workflow dans `_bmad/_config/workflow-manifest.csv`
3. **Créer la commande IDE** dans `.cursor/commands/`, `.claude/commands/`, etc.
4. **Lancer** via `/bmad-nom-du-workflow` dans un nouveau chat

Chaque workflow fournit dans son README les lignes exactes à copier-coller pour les étapes 2 et 3.

> Pour le guide complet avec les templates par IDE, voir [docs/getting-started.md](docs/getting-started.md).

## Prérequis

- Un projet utilisant la [BMAD Method](https://github.com/bmadcode/BMAD-METHOD) (v6+)
- Un IDE assisté par IA (Claude Code, Cursor, Windsurf, etc.)
- Un dossier `_bmad/` existant dans votre projet

## Structure du Dépôt

```text
BMAD_Customs_Workflows/
|-- README.md
|-- CONTRIBUTING.md
|-- LICENSE
|-- docs/
|   |-- getting-started.md
|   `-- workflow-anatomy.md
`-- workflows/
    |-- README.md               # Convention de classement (stable/incubation)
    |-- stable/                 # Workflows validés (vide pour le moment)
    `-- incubation/             # Workflows en cours de test et de création
        |-- dev-checkpoint/
        `-- smart-commit/
```

## Comment Fonctionnent les Workflows

Chaque workflow suit l'**architecture micro-fichiers BMAD** :

1. **`workflow.md`** est le point d'entrée — il définit l'objectif, le rôle et les règles
2. **Les fichiers d'étapes** dans `steps-c/` sont chargés un à la fois (chargement juste-à-temps)
3. Les étapes s'exécutent séquentiellement — pas de saut ni de réordonnancement
4. La progression est suivie dans le frontmatter des fichiers de sortie
5. Les menus à la fin de chaque étape vous permettent de contrôler le rythme

> Pour une compréhension approfondie, voir [docs/workflow-anatomy.md](docs/workflow-anatomy.md).

## Contribuer

Les contributions sont les bienvenues ! Si vous avez construit un workflow BMAD utile, envisagez de le partager.

Voir [CONTRIBUTING.md](CONTRIBUTING.md) pour les directives.

## Licence

Ce projet est sous licence MIT — voir [LICENSE](LICENSE) pour les détails.

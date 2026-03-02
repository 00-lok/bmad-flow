# Contribuer

Merci de votre intérêt pour la contribution de workflows BMAD personnalisés ! Ce guide explique comment soumettre votre propre workflow à cette collection.

## Avant de Commencer

Assurez-vous que votre workflow :

1. **Résout un vrai problème** — Il doit combler un manque dans la boîte à outils BMAD standard
2. **Est réutilisable** — Il doit fonctionner sur n'importe quel projet BMAD, pas seulement le vôtre
3. **Respecte les conventions BMAD** — Utilise l'architecture micro-fichiers, le suivi d'état et le système de menus
4. **Est testé** — Vous l'avez utilisé avec succès sur au moins un projet

## Exigences pour les Workflows

### Structure des Fichiers

Votre workflow doit suivre cette structure :

```
votre-workflow/
├── README.md                # Obligatoire — documentation pour les utilisateurs
├── workflow.md              # Obligatoire — point d'entrée
├── workflow-plan.md         # Recommandé — justification de la conception
├── data/                    # Optionnel — templates, schémas
│   └── ...
└── steps-c/                 # Obligatoire — fichiers d'étapes
    ├── step-01-init.md
    ├── step-01b-continue.md # Obligatoire si continuable
    ├── step-02-*.md
    └── ...
```

### Exigences du README

Le README de votre workflow doit inclure :

- **Le Problème** — Quel problème cela résout-il ?
- **Ce qu'il fait** — Aperçu étape par étape
- **Ce que vous obtenez** — Fichiers de sortie et leur utilité
- **Installation complète** — Les 4 étapes : copier, manifeste, commande IDE, lancer
- **Ligne de manifeste CSV** — Ligne exacte prête à copier-coller pour `workflow-manifest.csv`
- **Templates de commande IDE** — Templates pré-remplis pour Cursor, Claude, Gemini, GitHub Copilot
- **Comment le lancer** — Commande et déclencheurs en langage naturel
- **Quand l'utiliser** — Scénarios où ce workflow est précieux
- **Info Module** — Module cible, type de session, config requise

### Conventions des Workflows

- Utiliser le frontmatter dans tous les fichiers `.md`
- Inclure `MANDATORY EXECUTION RULES` dans chaque étape
- Inclure `SYSTEM SUCCESS/FAILURE METRICS` dans chaque étape
- Terminer chaque étape par un menu qui interrompt l'exécution
- Suivre la progression dans le frontmatter `stepsCompleted`
- Utiliser la syntaxe `{variable}` pour les valeurs de config (pas de chemins en dur)
- Inclure des instructions de fallback pour les subprocess

### Checklist Qualité

Avant de soumettre, vérifiez :

- [ ] Tous les fichiers d'étapes suivent la structure standard
- [ ] Les variables sont utilisées au lieu de valeurs en dur
- [ ] Chaque étape a des métriques de succès/échec claires
- [ ] Les menus interrompent l'exécution et attendent l'entrée utilisateur
- [ ] Le workflow est reprise possible (step-01b gère la continuation) — sauf si single-session
- [ ] Le README est complet et clair
- [ ] Aucun contenu spécifique à un projet ne subsiste
- [ ] La ligne de manifeste CSV est fournie dans le README (prête à copier-coller)
- [ ] Les templates de commande IDE sont fournis pour au moins Cursor et Claude Code
- [ ] Le module cible et la config requise sont clairement indiqués
- [ ] Le workflow est ajouté dans `workflows/incubation/` (puis promu vers `workflows/stable/` une fois validé)

## Comment Soumettre

### 1. Forkez ce Dépôt

Forkez ce dépôt et créez une branche pour votre workflow.

### 2. Ajoutez Votre Workflow

Placez le dossier de votre workflow dans `workflows/incubation/` :

```
workflows/
├── stable/                # Workflows validés (vide tant qu'aucun workflow n'est promu)
└── incubation/            # Workflows en test/création
    ├── dev-checkpoint/
    ├── smart-commit/
    └── votre-workflow/    # Nouveau workflow
```

Une fois validé (tests + qualité + documentation), déplacez-le vers `workflows/stable/`.

### 3. Mettez à Jour le README Principal

Ajoutez votre workflow au tableau dans le `README.md` racine :

```markdown
| [votre-workflow](workflows/incubation/votre-workflow/) | Module | Description | Quand l'utiliser... |
```

### 4. Vérifiez les Instructions d'Intégration

Assurez-vous que le README de votre workflow contient :

- La **ligne de manifeste CSV exacte** pour `_bmad/_config/workflow-manifest.csv`
- Les **templates de commande IDE pré-remplis** (au minimum Cursor et Claude Code)
- Le **chemin de destination** pour la copie du workflow (ex. `_bmad/core/workflows/nom/`)

Un utilisateur doit pouvoir intégrer votre workflow en suivant **uniquement** le README, sans consulter d'autre documentation.

### 5. Ouvrez une Pull Request

Incluez dans la description de votre PR :

- Quel problème le workflow résout
- Comment vous l'avez testé
- Quel module BMAD il cible

## Guide de Style

### Nommage

- Dossier du workflow : `kebab-case` (ex. `dev-checkpoint`, `smart-commit`)
- Fichiers d'étapes : `step-XX-nom.md` (ex. `step-01-init.md`, `step-02-analysis.md`)
- Fichiers de sortie : `nom-descriptif.md` (ex. `codebase-analysis.md`)

### Langue

- Les instructions des workflows peuvent être dans n'importe quelle langue
- Le README devrait être dans la langue du projet
- Utiliser la variable `{communication_language}` pour le changement de langue à l'exécution

### Ton

- Instructions des étapes : Direct, impératif ("Scanner le projet", "Présenter les résultats")
- READMEs : Clair, accessible, sans jargon inutile
- Métriques d'erreur : Spécifiques ("Ne pas lire le fichier complet" et non "Mal faire")

## Questions ?

Ouvrez une issue si vous avez des questions sur la contribution ou si vous avez besoin d'aide pour structurer votre workflow.

---
name: 'step-01b-continue'
description: 'Gérer la continuation du workflow depuis une session précédente'

outputFolder: '{output_folder}/dev-checkpoints'
nextStepOptions:
  step-02: './step-02-codebase-analysis.md'
  step-03: './step-03-artifacts-analysis.md'
  step-04: './step-04-diagnostic.md'
  step-05: './step-05-decisions.md'
  step-06: './step-06-application.md'
  step-07: './step-07-snapshot.md'
---

# Étape 1b : Continuer le Workflow

## OBJECTIF DE L'ÉTAPE :

Reprendre le workflow dev-checkpoint là où il a été interrompu lors d'une session précédente en lisant l'état de checkpoint-summary.md et en acheminant vers la bonne étape suivante.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE EN PREMIER) :

### Règles Universelles :

- 🛑 JAMAIS générer de contenu sans saisie utilisateur
- 📖 CRITIQUE : Lire le fichier d'étape complet avant toute action
- 🔄 CRITIQUE : Lors du chargement de l'étape suivante avec 'C', s'assurer que le fichier entier est lu
- 📋 VOUS ÊTES UN FACILITATEUR, pas un générateur de contenu
- ✅ VOUS DEVEZ TOUJOURS PARLER EN SORTIE dans {communication_language}

### Rappel du Rôle :

- ✅ Vous êtes un analyste technique reprenant un checkpoint en cours
- ✅ Direct et efficace — l'objectif est de reprendre rapidement

### Règles Spécifiques à l'Étape :

- 🎯 Se concentrer UNIQUEMENT sur la lecture de l'état et l'acheminement vers la bonne étape
- 🚫 INTERDIT de refaire les étapes déjà complétées
- 💬 Brève bienvenue, puis acheminement efficace

## LIMITES DU CONTEXTE :

- L'utilisateur a déjà exécuté ce workflow
- checkpoint-summary.md existe avec le tableau stepsCompleted
- Besoin d'acheminer vers la bonne étape suivante
- Tous les fichiers générés précédemment (codebase-analysis.md, etc.) devraient encore exister dans le dossier checkpoint

## SÉQUENCE OBLIGATOIRE

**CRITIQUE :** Suivre cette séquence exactement.

### 1. Trouver le Checkpoint en Cours

Rechercher dans {outputFolder} le checkpoint-summary.md le plus récent avec `status: IN_PROGRESS`.

Charger ce fichier et lire son frontmatter :
- Tableau `stepsCompleted`
- `lastStep`
- `checkpointFolder`
- `artifactsDiscovered`

### 2. Bienvenue

"**Bienvenue, {user_name} ! Le BMad Master reprend votre checkpoint en cours.**

- **Dossier :** {checkpointFolder}
- **Dernière étape complétée :** {lastStep}
- **Étapes terminées :** {stepsCompleted}

Prêt à reprendre à l'étape suivante."

### 3. Déterminer l'Étape Suivante

En fonction de la dernière étape complétée dans `stepsCompleted`, identifier l'étape suivante à exécuter :

- Si dernière était `step-01-init` → suivante est `step-02-codebase-analysis`
- Si dernière était `step-02-codebase-analysis` → suivante est `step-03-artifacts-analysis`
- Si dernière était `step-03-artifacts-analysis` → suivante est `step-04-diagnostic`
- Si dernière était `step-04-diagnostic` → suivante est `step-05-decisions`
- Si dernière était `step-05-decisions` → suivante est `step-06-application`
- Si dernière était `step-06-application` → suivante est `step-07-snapshot`

### 4. Acheminer vers la Bonne Étape

Charger, lire entièrement, puis exécuter le fichier d'étape approprié depuis {nextStepOptions}.

---

## 🚨 MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### ✅ SUCCÈS :

- Checkpoint en cours trouvé et état lu
- Utilisateur accueilli avec un statut clair
- Bonne étape suivante identifiée et chargée
- Aucune étape ré-exécutée

### ❌ ÉCHEC DU SYSTÈME :

- Ré-exécuter les étapes complétées
- Ne pas lire stepsCompleted depuis le frontmatter
- Acheminer vers la mauvaise étape
- Ne pas trouver le checkpoint en cours

**Règle Maîtresse :** Sauter des étapes, optimiser les séquences ou ne pas suivre les instructions exactes est INTERDIT et constitue un ÉCHEC DU SYSTÈME.

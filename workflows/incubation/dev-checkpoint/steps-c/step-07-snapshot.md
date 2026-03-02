---
name: 'step-07-snapshot'
description: 'Finaliser le résumé du checkpoint avec une vue d\'ensemble lisible et marquer le workflow comme terminé'

checkpointFolder: '{checkpointFolder}'
---

# Étape 7 : Snapshot Final

## OBJECTIF DE L'ÉTAPE :

Finaliser le checkpoint en complétant le `checkpoint-summary.md` avec un résumé complet et lisible qui donne à quiconque une vision claire de l'état du projet, des actions de réalignement effectuées et de la suite. Marquer le workflow comme terminé.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE EN PREMIER) :

### Règles Universelles :

- 🛑 NE JAMAIS générer de contenu sans entrée utilisateur
- 📖 CRITIQUE : Lire le fichier d'étape complet avant toute action
- 🔄 CRITIQUE : Lors du chargement de l'étape suivante avec 'C', s'assurer que le fichier entier est lu
- 📋 VOUS ÊTES UN FACILITATEUR, pas un générateur de contenu
- ✅ VOUS DEVEZ TOUJOURS PARLER EN SORTIE dans {communication_language}

### Rappel du Rôle :

- ✅ Vous êtes un communicateur technique produisant un résumé clair et actionnable
- ✅ Clair, accessible, synthétique. Écrit pour être compris par quelqu'un qui n'a pas suivi le processus.
- ✅ Vous apportez une expertise en synthèse d'informations techniques complexes en résumés digestibles

### Règles Spécifiques à l'Étape :

- 🎯 Synthèse finale — claire, lisible, human-friendly
- 🚫 INTERDIT d'utiliser du jargon sans explication
- 💬 Écrire comme si le lecteur découvre l'état du projet pour la première fois
- 📋 Inclure une évaluation qualitative de la santé du projet

## PROTOCOLES D'EXÉCUTION :

- 🎯 Suivre la SÉQUENCE OBLIGATOIRE exactement
- 💾 Finaliser checkpoint-summary.md avec toutes les sections
- 📖 Marquer le workflow comme TERMINÉ dans le frontmatter
- 🚫 C'est l'étape FINALE — pas de nextStepFile

## LIMITES DU CONTEXTE :

- Disponible : Tous les fichiers du checkpoint (codebase-analysis, artifacts-review, misalignment-report, decisions-log, action-items)
- Focus : Synthèse et finalisation
- Limites : Résumer et synthétiser, ne pas créer de nouvelle analyse
- Dépendances : Toutes les étapes précédentes terminées

## SÉQUENCE OBLIGATOIRE

**CRITIQUE :** Suivre cette séquence exactement. Ne pas sauter, réordonner ou improviser sauf demande explicite de l'utilisateur.

### 1. Charger Tous les Fichiers du Checkpoint

Lire tous les fichiers dans {checkpointFolder} :
- `codebase-analysis.md`
- `artifacts-review.md`
- `misalignment-report.md`
- `decisions-log.md`
- `action-items.md`

### 2. Générer l'Évaluation de Santé du Projet

Sur la base de toute l'analyse, déterminer un score de santé global du projet :

- **🟢 Aligné** — Le projet est bien aligné avec la documentation. Divergences mineures seulement.
- **🟡 Partiellement aligné** — Des divergences significatives existent mais le projet reste sur la bonne trajectoire.
- **🔴 Besoin d'attention** — Des divergences critiques nécessitent une action immédiate.

### 3. Finaliser le Résumé du Checkpoint

Mettre à jour `{checkpointFolder}/checkpoint-summary.md` — remplacer les sections placeholder par le contenu complet :

```markdown
# Dev Checkpoint — {project_name}

## Date: {date}

## 🏥 Santé du projet : [🟢/🟡/🔴] [Aligné / Partiellement aligné / Besoin d'attention]

---

## Résumé Human-Friendly

### Où en est le projet ?

[2-3 paragraphes en langage clair décrivant l'état actuel du projet :
- Ce qui est fait et fonctionne bien
- Ce qui est en cours de développement
- Ce qui reste à faire par rapport à la vision initiale
- Le pourcentage approximatif d'avancement global]

### Ce qui a été réaligné lors de ce checkpoint

[Liste claire des changements apportés à la documentation :
- Quels artefacts ont été mis à jour
- Pourquoi (en langage simple)
- Ce que ça change pour la suite du développement]

### Ce qui reste à faire

[Liste priorisée des actions correctives sur le code :
- Actions critiques à traiter en premier
- Actions importantes pour la prochaine itération
- Actions mineures à planifier]

### Prochaines priorités recommandées

[3-5 recommandations concrètes sur ce qui devrait être fait en premier, basées sur l'analyse complète]

---

## Métriques du checkpoint

| Métrique | Valeur |
|----------|--------|
| Artefacts BMAD analysés | X |
| Désalignements identifiés | X |
| Dont critiques | X |
| Décisions prises | X |
| Artefacts mis à jour | X |
| Actions code restantes | X |

## Fichiers de ce checkpoint

| Fichier | Description |
|---------|-------------|
| checkpoint-summary.md | Ce résumé |
| codebase-analysis.md | Analyse complète du code source |
| artifacts-review.md | Revue de tous les artefacts BMAD |
| misalignment-report.md | Inventaire des désalignements |
| decisions-log.md | Journal des décisions de réalignement |
| action-items.md | Actions correctives à planifier |

## Contexte du développeur

[Réponses de l'étape 01 — préservées depuis l'initialisation]

## Artefacts BMAD découverts

[Liste de l'étape 01 — préservée depuis l'initialisation]
```

### 4. Mettre à Jour le Frontmatter pour Terminer

Mettre à jour le frontmatter de `checkpoint-summary.md` :
- Ajouter `step-07-snapshot` à `stepsCompleted`
- Définir `lastStep: 'step-07-snapshot'`
- Définir `status: COMPLETE`

### 5. Présenter le Résumé Final au Développeur

Présenter le résumé lisible directement au développeur :

"**✅ Dev Checkpoint terminé !**

**🏥 Santé du projet : [score]**

[Présenter les sections clés du résumé lisible]

**Dossier du checkpoint :** `{checkpointFolder}/`

Tous les fichiers de synthèse sont disponibles dans ce dossier. Vos artefacts BMAD ont été mis à jour et votre contexte projet est maintenant réaligné.

Le BMad Master recommande de relancer un checkpoint après la prochaine phase de développement significative pour maintenir l'alignement."

---

## 🚨 MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### SUCCÈS :

- Tous les fichiers du checkpoint lus et synthétisés
- Évaluation de santé du projet déterminée et justifiée
- Résumé lisible rédigé en langage clair et accessible
- Tableau des métriques rempli avec des chiffres exacts
- checkpoint-summary.md finalisé avec toutes les sections
- Statut marqué comme TERMINÉ
- Développeur présenté avec un résumé final clair

### ÉCHEC SYSTÈME :

- Résumé utilisant du jargon sans explication
- Sections manquantes dans checkpoint-summary.md
- Ne pas lire tous les fichiers du checkpoint avant de synthétiser
- Statut non marqué comme TERMINÉ
- Résumé inutile pour quelqu'un le lisant pour la première fois

**Règle Maîtresse :** Le résumé final doit être assez clair pour que quiconque le lisant comprenne l'état exact du projet. Pas de jargon, pas de présomptions.

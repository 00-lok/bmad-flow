---
name: 'step-02-codebase-analysis'
description: 'Analyse autonome approfondie du code source - structure, qualité, patterns, dépendances, historique git'

nextStepFile: './step-03-artifacts-analysis.md'
checkpointFolder: '{checkpointFolder}'
---

# Étape 2 : Analyse du Code Source

## OBJECTIF DE L'ÉTAPE :

Réaliser une analyse autonome et complète de l'ensemble du code source — structure, qualité du code, patterns architecturaux, dépendances, historique git et dette technique — produisant un rapport détaillé `codebase-analysis.md` dans le dossier checkpoint.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE EN PREMIER) :

### Règles Universelles :

- 🛑 JAMAIS générer de contenu sans saisie utilisateur
- 📖 CRITIQUE : Lire le fichier d'étape complet avant toute action
- 🔄 CRITIQUE : Lors du chargement de l'étape suivante avec 'C', s'assurer que le fichier entier est lu
- 📋 VOUS ÊTES UN FACILITATEUR, pas un générateur de contenu
- ✅ VOUS DEVEZ TOUJOURS PARLER EN SORTIE dans {communication_language}
- ⚙️ REPLI OUTIL/SOUS-PROCESSUS : Si une instruction fait référence à un sous-processus, sous-agent ou outil auquel vous n'avez pas accès, vous DEVEZ malgré tout atteindre le résultat dans votre fil de contexte principal

### Rappel du Rôle :

- ✅ Vous êtes un expert en revue de code et architecte logiciel
- ✅ Direct, factuel, exhaustif. Analyse en profondeur, pas en surface.
- ✅ Vous apportez une expertise approfondie en qualité du code, patterns d'architecture et évaluation de la dette technique

### Règles Spécifiques à l'Étape :

- 🎯 Analyse approfondie et autonome — prendre le temps nécessaire pour tout capter
- 🚫 INTERDIT de comparer avec les artefacts BMAD dans cette étape — la comparaison se fait à l'étape 04
- 💬 Pattern Sous-processus 2+4 : Utiliser les sous-agents en parallèle pour différentes zones d'analyse
- ⚙️ Si sous-processus indisponible, effectuer toute l'analyse séquentiellement dans le fil principal
- 🚫 NE PAS ÊTRE PARESSEUX — analyser chaque zone significative du code source

## PROTOCOLES D'EXÉCUTION :

- 🎯 Suivre la SÉQUENCE OBLIGATOIRE exactement
- 💾 Écrire l'analyse complète dans {checkpointFolder}/codebase-analysis.md
- 📖 Mettre à jour stepsCompleted dans checkpoint-summary.md
- 🚫 NE PAS sauter de zone d'analyse — la rigueur est critique

## LIMITES DU CONTEXTE :

- Disponible : checkpoint-summary.md avec artifactsDiscovered et contexte développeur de l'étape 01
- Focus : Code source UNIQUEMENT — pas encore de comparaison avec les artefacts
- Limites : Analyser ce qui existe, ne pas prescrire de changements
- Dépendances : step-01-init complétée, dossier checkpoint existe

## SÉQUENCE OBLIGATOIRE

**CRITIQUE :** Suivre cette séquence exactement. Ne pas sauter, réordonner ou improviser sauf si l'utilisateur demande explicitement un changement.

### 1. Annoncer le Démarrage de l'Analyse

"**Lancement de l'analyse approfondie du code source.**
Cette phase est majoritairement autonome. Le BMad Master va scanner l'ensemble du projet. Cela peut prendre un moment."

### 2. Analyse de la Structure du Projet

Scanner l'ensemble de la structure du projet :

- Arborescence des répertoires et pattern d'organisation (monorepo, modulaire, par fonctionnalité, par couches...)
- Répertoires clés et leurs rôles
- Nombre et répartition des fichiers par type
- Points d'entrée et fichiers de configuration
- Identifier le pattern architectural utilisé (FSD, MVC, hexagonal, etc.)

### 3. Revue de la Qualité du Code

NE PAS ÊTRE PARESSEUX — Pour CHAQUE zone significative du code source, lancer un sous-processus (ou analyser séquentiellement si indisponible) qui :

1. Lit les fichiers de code de cette zone
2. Analyse :
   - Conventions et cohérence du code (nommage, formatage, structure)
   - Organisation et cohésion des composants/modules
   - Patterns de gestion des erreurs
   - Sécurité des types et couverture du typage
   - Duplication de code et conformité DRY
   - Évaluation de la complexité (imbrication profonde, fonctions longues, fichiers volumineux)
3. Retourne des constats structurés : conventions utilisées, problèmes de qualité trouvés, patterns identifiés

**Zones à analyser (adapter au projet) :**
- Composants / couche UI
- Logique métier / services / utilitaires
- Couche données (appels API, gestion d'état, base de données)
- Configuration et infrastructure
- Tests (si présents)

### 4. Analyse de la Stack et des Dépendances

Analyser la stack technique :

- Versions du framework et du runtime
- Dépendances clés et leurs versions
- Dépendances de développement et outils
- Identifier les dépendances obsolètes ou potentiellement problématiques
- Configuration et scripts de build
- Patterns de configuration d'environnement

### 5. Analyse de l'Historique Git

Analyser l'historique git récent pour comprendre l'évolution :

- Patterns et fréquence des commits récents
- Zones de développement les plus actives
- Contributeurs et leurs domaines de focus
- Tout refactoring ou pivot significatif visible dans l'historique
- Structure des branches si pertinent

### 6. Identification de la Dette Technique

Sur la base de l'analyse ci-dessus, identifier la dette technique :

- Problèmes de qualité du code qui accumulent des coûts
- Tests manquants ou lacunes de couverture
- Valeurs codées en dur, nombres magiques
- Commentaires TODO/FIXME/HACK
- Patterns incohérents dans le code source
- Dépendances à mettre à jour
- Configuration à nettoyer

### 7. Rédiger le Rapport d'Analyse du Code Source

Créer `{checkpointFolder}/codebase-analysis.md` avec le format semi-structuré suivant :

```markdown
# Analyse du Code Source

## Date: {date}

## Structure du projet
[Findings from step 2]

## Qualité du code
[Findings from step 3 — grouped by area]

## Stack technique et dépendances
[Findings from step 4]

## Historique Git
[Findings from step 5]

## Dette technique identifiée
[Findings from step 6 — prioritized]

## Métriques clés
- Nombre de fichiers: X
- Langages principaux: X
- Couverture de tests: X (si applicable)
- Zones critiques identifiées: X
```

### 8. Mettre à Jour la Synthèse du Checkpoint

Mettre à jour le frontmatter de `{checkpointFolder}/checkpoint-summary.md` :
- Ajouter `step-02-codebase-analysis` à `stepsCompleted`
- Définir `lastStep: 'step-02-codebase-analysis'`

### 9. Présenter le Résumé des Résultats

Présenter un bref résumé des constats clés au développeur :

"**Analyse du code terminée. Voici les points clés :**
- [3-5 constats les plus significatifs]
- [Tout signal d'alerte ou observation notable]

Le rapport complet est dans `codebase-analysis.md`. Prêt pour l'analyse des artefacts BMAD."

### 10. Présenter les OPTIONS DU MENU

Afficher : **[C] Continuer — Lancer l'analyse des artefacts BMAD**

#### Logique de Gestion du Menu :

- SI C : Vérifier que codebase-analysis.md est écrit et checkpoint-summary.md est mis à jour, puis charger, lire le fichier entier, puis exécuter {nextStepFile}
- SI Autre : aider l'utilisateur, puis réafficher le menu

#### RÈGLES D'EXÉCUTION :

- TOUJOURS s'arrêter et attendre la saisie utilisateur après présentation du menu
- NE passer à l'étape suivante QUE lorsque l'utilisateur sélectionne 'C'

---

## 🚨 MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### ✅ SUCCÈS :

- Structure du projet entièrement cartographiée et documentée
- Qualité du code revue dans toutes les zones significatives
- Stack et dépendances analysées
- Insights de l'historique Git capturés
- Dette technique identifiée et priorisée
- Rapport codebase-analysis.md complet écrit dans le dossier checkpoint
- stepsCompleted mis à jour dans checkpoint-summary.md

### ❌ ÉCHEC DU SYSTÈME :

- Analyse superficielle qui manque des zones significatives
- Être paresseux — sauter des zones de code ou faire une revue superficielle
- Comparer avec les artefacts BMAD (pas encore — c'est l'étape 04)
- Ne pas rédiger le rapport complet
- Ne pas mettre à jour checkpoint-summary.md

**Règle Maîtresse :** La rigueur est non négociable. Chaque zone significative du code source doit être analysée. Sauter des étapes est INTERDIT.

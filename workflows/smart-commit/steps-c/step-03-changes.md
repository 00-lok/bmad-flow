---
name: 'step-03-changes'
description: 'Analyse approfondie de tous les changements non commités avec catégorisation et cartographie des dépendances'

nextStepFile: './step-04-plan.md'
---

# Étape 3 : Analyse des Changements

## OBJECTIF DE L'ÉTAPE :

Effectuer une analyse approfondie de chaque changement non commité — comprendre ce qui a été modifié, catégoriser chaque changement par type et domaine, identifier les regroupements logiques et cartographier les dépendances entre les changements.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE D'ABORD) :

### Règles Universelles :

- CRITIQUE : Lire le fichier d'étape complet avant toute action
- CRITIQUE : Lors du chargement de l'étape suivante avec 'C', s'assurer que le fichier entier est lu

### Règles Spécifiques à l'Étape :

- Cette étape est AUTONOME — analyser tous les changements sans saisie utilisateur
- Ne PAS modifier de fichiers pendant cette étape
- Analyser CHAQUE fichier modifié — aucun fichier ne peut être ignoré
- Être précis dans la catégorisation — cela détermine directement la qualité du plan de commits

## PROTOCOLES D'EXÉCUTION :

### Optimisation des Sous-processus (si disponible) :

- Utiliser des sous-agents parallèles pour analyser des groupes de fichiers simultanément
- Chaque sous-agent analyse un sous-ensemble de fichiers et retourne : chemin du fichier, type de changement, scope, importance, fichiers liés
- Repli : traiter tous les fichiers séquentiellement dans le fil de contexte principal

## SÉQUENCE OBLIGATOIRE

### 1. Collecter l'Inventaire Complet des Changements

Rassembler la vue complète des changements non commités à l'aide de trois commandes :

- **Changements staged** : `git diff --cached --name-status`
- **Changements unstaged** : `git diff --name-status`
- **Fichiers untracked** : `git ls-files --others --exclude-standard`

Construire une liste unifiée de TOUS les fichiers avec leur statut git :
- **A** = Added (nouveau fichier, staged)
- **M** = Modified
- **D** = Deleted
- **R** = Renamed
- **?** = Untracked (nouveau, non staged)

### 2. Analyser Chaque Fichier Modifié

Pour chaque fichier de l'inventaire, déterminer :

**a) Comprendre le changement :**
- Pour les **fichiers modifiés** : examiner `git diff <file>` (ou `git diff --cached <file>`) — comprendre ce qui a spécifiquement changé, pas seulement qu'il a changé
- Pour les **fichiers nouveaux/untracked** : lire le fichier pour comprendre son but et son contenu
- Pour les **fichiers supprimés** : noter ce qui a été retiré via `git show HEAD:<file>` si nécessaire
- Pour les **fichiers renommés** : noter les anciens et nouveaux noms, vérifier les changements de contenu

**b) Classifier le changement :**
- **Type de changement** (un parmi) : `feat`, `fix`, `refactor`, `docs`, `style`, `test`, `chore`, `config`, `build`, `ci`, `perf`
- **Scope/domaine** : à quelle zone du projet ce changement appartient (ex. auth, api, ui, database, config, tooling)
- **Importance** : `major` (changement structurel, nouvelle capacité), `minor` (amélioration, mise à jour), `trivial` (formatage, typo, commentaire)

**c) Cartographier les relations :**
- Quels autres fichiers modifiés sont logiquement liés à celui-ci ?
- Ce fichier dépend-il d'un autre fichier modifié ou un autre en dépend-il ?

### 3. Identifier les Regroupements Logiques

Regrouper les changements liés selon ces critères (par ordre de priorité) :

1. **Cohésion fonctionnelle** — Fichiers qui implémentent la même fonctionnalité, corrigent le même bug ou servent le même objectif de refactoring
2. **Chaînes de dépendance** — Fichiers qui DOIVENT être commités ensemble pour que la base de code reste cohérente (ex. une nouvelle définition de type + le code qui l'importe)
3. **Proximité de domaine** — Fichiers du même module ou composant modifiés pour la même raison
4. **Alignement du type de changement** — Même type de changement dans des zones indépendantes (ex. toutes les mises à jour de documentation, tous les changements de config)

Pour chaque groupe, assigner :
- Une étiquette préliminaire (deviendra la base du message de commit)
- La liste des fichiers
- Le type de changement qui représente le mieux le groupe
- Toute contrainte d'ordre par rapport aux autres groupes

### 4. Détecter les Contraintes d'Ordre des Commits

Identifier quels groupes doivent précéder les autres :

- Changements infrastructure/config → avant le code qui en dépend
- Changements schéma/modèle/types → avant le code qui utilise les nouveaux champs ou types
- Utilitaires ou bibliothèques partagés → avant les fonctionnalités qui les importent
- Composants de base → avant les composants composés
- Implémentation → avant ou avec les tests de cette implémentation
- Documentation → typiquement en dernier sauf si elle fait partie d'une fonctionnalité

### 5. Présenter le Résumé des Changements

Afficher une vue d'ensemble structurée :

**Statistiques des Changements :**
- Total fichiers : X (Y ajoutés, Z modifiés, W supprimés, V untracked)

**Regroupements Identifiés :**
Pour chaque groupe :
- Étiquette du groupe et type de changement
- Fichiers du groupe (avec indicateur de statut)
- Contraintes d'ordre (le cas échéant)

**Notes sur les Dépendances :**
- Toute chaîne de dépendance notable ou exigence d'ordre

### 6. Présenter les OPTIONS DU MENU

Afficher : **[C] Continuer — Générer le plan de commits**

#### Logique de Gestion du Menu :

- SI C : Charger, lire le fichier entier, puis exécuter {nextStepFile}
- SI Autre : Expliquer l'option, puis réafficher le menu

#### RÈGLES D'EXÉCUTION :

- TOUJOURS s'arrêter et attendre la saisie utilisateur après avoir présenté le menu
- Ne passer à l'étape suivante QUE lorsque l'utilisateur sélectionne 'C'

## MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### SUCCÈS :

- Chaque fichier modifié analysé, catégorisé et assigné à un groupe
- Les regroupements logiques reflètent de véritables relations fonctionnelles
- Contraintes de dépendance identifiées et documentées
- Résumé complet présenté

### ÉCHEC :

- Fichiers ignorés ou non analysés
- Catégorisation vague ou incohérente
- Dépendances manquées — pourrait conduire à des commits intermédiaires cassés
- Regroupements arbitraires plutôt que logiquement motivés

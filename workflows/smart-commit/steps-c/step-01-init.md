---
name: 'step-01-init'
description: 'Vérifier le dépôt git, détecter les changements non commités et préparer l''analyse'

nextStepFile: './step-02-context.md'
---

# Étape 1 : Initialisation

## OBJECTIF DE L'ÉTAPE :

Vérifier que le projet est un dépôt git avec des changements non commités, établir les informations de base et préparer l'analyse.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE D'ABORD) :

### Règles Universelles :

- CRITIQUE : Lire le fichier d'étape complet avant toute action
- CRITIQUE : Lors du chargement de l'étape suivante, s'assurer que le fichier entier est lu

### Règles Spécifiques à l'Étape :

- Si aucun dépôt git n'est détecté, ARRÊTER le workflow et informer l'utilisateur
- Si aucun changement non commité n'est trouvé, ARRÊTER le workflow et informer l'utilisateur
- Cette étape se poursuit automatiquement — pas d'interaction menu sauf en cas d'erreur

## SÉQUENCE OBLIGATOIRE

### 1. Vérifier le Dépôt Git

Exécuter `git rev-parse --is-inside-work-tree` pour confirmer que le répertoire courant est à l'intérieur d'un dépôt git.

**SI ce n'est PAS un dépôt git :**
Afficher : "⛔ Ce répertoire n'est pas un dépôt Git. Le workflow smart-commit nécessite un dépôt Git initialisé."
ARRÊTER le workflow — ne pas poursuivre.

### 2. Détecter les Changements Non Commités

Exécuter `git status --porcelain` pour vérifier la présence de changements non commités (staged, unstaged, untracked).

**SI aucun changement détecté :**
Afficher : "✅ Aucun changement non commité détecté. L'arbre de travail est propre — rien à commiter."
ARRÊTER le workflow — ne pas poursuivre.

### 3. Établir la Base de Référence

Collecter les informations de base :

- **Racine du dépôt** : `git rev-parse --show-toplevel`
- **Branche courante** : `git branch --show-current`
- **Statut de suivi** : `git status -sb` (ahead/behind remote)
- **Comptage des changements** : Compter les fichiers staged, unstaged et untracked à partir de la sortie porcelain

### 4. Afficher le Résumé de Bienvenue

Afficher :

- Salutation utilisant {user_name}
- Chemin de la racine du dépôt
- Nom de la branche courante et statut de suivi
- Aperçu des changements : X fichiers staged, Y unstaged, Z untracked
- "Le BMad Master va analyser votre projet et préparer un plan de commits intelligent."

### 5. Poursuite Automatique

Charger, lire le fichier entier, puis exécuter {nextStepFile}.

## MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### SUCCÈS :

- Dépôt git confirmé
- Changements non commités détectés
- Informations de base collectées
- Résumé de bienvenue affiché
- Poursuite automatique vers l'étape 02

### ÉCHEC :

- Pas de dépôt git — workflow arrêté
- Aucun changement non commité — workflow arrêté

---
name: 'step-02-context'
description: 'Analyser la structure du projet et l''historique git pour construire un contexte complet pour la planification des commits'

nextStepFile: './step-03-changes.md'
---

# Étape 2 : Analyse du Contexte

## OBJECTIF DE L'ÉTAPE :

Construire une compréhension complète de la structure du projet et des conventions de commit git pour informer la planification intelligente des commits dans les étapes suivantes.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE D'ABORD) :

### Règles Universelles :

- CRITIQUE : Lire le fichier d'étape complet avant toute action
- CRITIQUE : Lors du chargement de l'étape suivante avec 'C', s'assurer que le fichier entier est lu

### Règles Spécifiques à l'Étape :

- Cette étape est AUTONOME — exécuter toute l'analyse sans saisie utilisateur
- Ne PAS modifier de fichiers pendant cette étape
- Stocker tous les résultats d'analyse en mémoire pour utilisation dans les étapes suivantes
- Se concentrer sur les informations directement pertinentes pour la planification des commits

## SÉQUENCE OBLIGATOIRE

### 1. Analyse de la Structure du Projet

Analyser le projet pour comprendre sa nature et son organisation :

- **Détection de la pile technique** — Examiner les fichiers package/dépendances pour identifier les langages, frameworks et outils :
  - JavaScript/TypeScript : `package.json`, `tsconfig.json`
  - Python : `requirements.txt`, `pyproject.toml`, `setup.py`
  - Rust : `Cargo.toml` | Go : `go.mod` | Java : `pom.xml`, `build.gradle`
  - Autres : scanner les extensions de fichiers et les configs de build
- **Organisation du projet** — Identifier le schéma de structure des répertoires (monorepo, `src/`, `app/`, `lib/`, modulaire, plat)
- **Domaines fonctionnels** — Cartographier les répertoires de premier niveau vers les domaines fonctionnels (ex. `api/`, `components/`, `models/`, `tests/`)

### 2. Détection des Conventions de Commit Git

Analyser les 25 derniers commits pour détecter le style de commit du projet :

- Exécuter `git log --format="%s" -25` pour extraire les messages de commit
- **Conventional Commits** — Vérifier le motif `type(scope): description` (ex. `feat(auth): add login`)
- **Motifs de préfixe** — Vérifier les styles `[TYPE]`, `TYPE:`, `type -`
- **Emoji/Gitmoji** — Vérifier les messages préfixés par emoji
- **Références de ticket** — Vérifier les motifs `#123`, `JIRA-456`, `PROJ-789`
- **Aucune convention** — Si aucun motif cohérent, noter "aucune convention détectée — utilisation de Conventional Commits par défaut"
- **Langue des messages** — Déterminer si les messages sont en anglais, français ou mixte
- **Granularité** — Évaluer la taille typique des commits : atomique (petit, une seule préoccupation) vs. groupé (grand, multi-préoccupations)

### 3. Synthèse des Conventions de Commit

Synthétiser la convention détectée en un ensemble de règles claires :

- **Type de convention** : nom du motif détecté
- **Modèle de format** : le format exact à suivre (ex. `type(scope): description`)
- **Types disponibles** : liste des types utilisés dans l'historique (feat, fix, refactor, docs, etc.)
- **Utilisation du scope** : si les scopes sont utilisés et ce qu'ils représentent
- **Langue** : la langue à utiliser pour les messages de commit
- **Exemples** : 3 commits représentatifs de l'historique illustrant au mieux la convention

### 4. Présenter le Résumé du Contexte

Afficher les résultats d'analyse à l'utilisateur dans un format clair et organisé :

**Contexte du Projet :**
- Type de projet, pile technique, langage(s) principal(aux)
- Organisation des répertoires et domaines clés

**Convention de Commit Détectée :**
- Nom de la convention et modèle de format
- Types disponibles et motifs de scope
- Langue des messages
- 3 exemples de commits de l'historique

**Contexte de Branche :**
- Branche courante et statut de suivi (depuis l'étape 01)

### 5. Présenter les OPTIONS DU MENU

Afficher : **[C] Continuer — Lancer l'analyse des changements**

#### Logique de Gestion du Menu :

- SI C : Charger, lire le fichier entier, puis exécuter {nextStepFile}
- SI Autre : Expliquer l'option, puis réafficher le menu

#### RÈGLES D'EXÉCUTION :

- TOUJOURS s'arrêter et attendre la saisie utilisateur après avoir présenté le menu
- Ne passer à l'étape suivante QUE lorsque l'utilisateur sélectionne 'C'

## MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### SUCCÈS :

- Structure du projet analysée et pile technique identifiée
- Convention de commit détectée (ou défaut choisi) avec des règles de format claires
- Langue des messages déterminée
- Résumé du contexte présenté à l'utilisateur

### ÉCHEC :

- Impossible d'accéder à l'historique git
- Détection de convention ambiguë sans résolution
- Analyse superficielle ou motifs clés manqués

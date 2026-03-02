---
name: 'step-04-plan'
description: 'Générer un plan de commits intelligent à partir de l''analyse et le présenter pour validation utilisateur'

nextStepFile: './step-05-execute.md'
---

# Étape 4 : Plan de Commits

## OBJECTIF DE L'ÉTAPE :

Synthétiser toute l'analyse (contexte projet, conventions de commit, inventaire des changements, regroupements et ordre des dépendances) en un plan de commits optimal. Présenter le plan pour validation utilisateur — c'est le point de décision principal du workflow.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE D'ABORD) :

### Règles Universelles :

- CRITIQUE : Lire le fichier d'étape complet avant toute action
- CRITIQUE : Lors du chargement de l'étape suivante, s'assurer que le fichier entier est lu

### Rappel du Rôle :

- VOUS ÊTES UN FACILITATEUR — présentez le plan clairement et respectez les décisions de l'utilisateur
- L'utilisateur a l'autorité finale sur le regroupement, l'ordre et la formulation des messages

### Règles Spécifiques à l'Étape :

- Le plan DOIT couvrir TOUS les fichiers modifiés — aucun fichier ne doit rester non commité
- Chaque commit doit être atomique : une seule préoccupation logique par commit
- Les messages de commit DOIVENT suivre les conventions détectées à l'étape 02
- Ne JAMAIS exécuter de commandes git dans cette étape — planification uniquement
- Si l'utilisateur demande des modifications, les appliquer et re-présenter le plan mis à jour

## SÉQUENCE OBLIGATOIRE

### 1. Générer le Plan de Commits

En utilisant les regroupements et l'ordre des dépendances de l'étape 03, et les conventions de commit de l'étape 02, générer le plan de commits optimal.

**Stratégie d'ordre des commits** (appliquer dans cet ordre de priorité) :

1. Configs infrastructure/environnement, CI/CD, outils de build
2. Changements de dépendances et packages
3. Schéma, modèles de données, définitions de types
4. Code partagé — utilitaires, helpers, composants partagés
5. Implémentations des fonctionnalités principales
6. Code périphérique — mises à jour liées, intégrations, adaptations
7. Tests — avec ou après le code qu'ils testent
8. Documentation — README, docs, docs inline
9. Style/nettoyage — formatage, linting, corrections triviales

**Pour chaque commit, déterminer :**

- **Liste exacte des fichiers** : chaque fichier inclus dans ce commit
- **Message de commit** : suivant la convention détectée à l'étape 02
  - Si Conventional Commits : `type(scope): description concise`
  - Si motif personnalisé : suivre le motif détecté exactement
  - Si aucune convention détectée : défaut `type(scope): description concise`
- **Justification** : brève explication de pourquoi ces fichiers vont ensemble

**Règles de qualité des messages de commit :**

- Correspondre à la langue utilisée dans les messages de commit existants du projet
- Première ligne sous 72 caractères
- Utiliser le présent, mode impératif (ex. "add", "fix", "update", pas "added", "fixed", "updated")
- Ajouter un paragraphe de corps (deuxième flag `-m`) uniquement quand le changement requiert une explication non évidente
- Le scope doit refléter le domaine identifié à l'étape 03

### 2. Valider la Complétude du Plan

Avant de présenter le plan, vérifier :

- [ ] Chaque fichier de l'inventaire des changements apparaît dans exactement un commit
- [ ] Aucun commit ne mélange des préoccupations non liées
- [ ] L'ordre respecte toutes les contraintes de dépendance de l'étape 03
- [ ] Les messages de commit sont cohérents en style, langue et format
- [ ] Aucun commit n'est vide et aucun commit n'est trop volumineux (signaler les commits avec >15 fichiers)

Si un commit dépasse 15 fichiers, envisager de le diviser davantage et expliquer la justification.

### 3. Présenter le Plan Complet

Afficher le plan de commits dans ce format :

---

**📋 Plan de commits — N commit(s) proposé(s)**

Pour chaque commit (numéroté 1 à N) :

**━━━ Commit X/N ━━━**
**Message :** `le message de commit`
**Fichiers (count) :**
- `[status]` path/to/file
- `[status]` path/to/other-file
**Raison :** brève justification de ce regroupement

Après tous les commits :

**━━━ Récapitulatif ━━━**
- Total : N commits, F fichiers
- Convention : nom de la convention détectée
- Ordre : Commit 1 → Commit 2 → ... → Commit N

---

### 4. Présenter les OPTIONS DU MENU

Afficher :

**Sélectionnez une option :**
- **[V]** Valider et exécuter le plan
- **[M]** Modifier le plan
- **[R]** Régénérer le plan depuis zéro
- **[X]** Annuler — quitter sans commiter

#### Logique de Gestion du Menu :

- **SI V** : Vérifier que le plan est complet et cohérent. Charger, lire le fichier entier, puis exécuter {nextStepFile}
- **SI M** : Demander à l'utilisateur ce qu'il souhaite modifier. Modifications possibles :
  - Déplacer un fichier d'un commit à un autre
  - Changer un message de commit
  - Réordonner les commits
  - Diviser un commit en deux
  - Fusionner deux commits en un
  Appliquer les modifications, puis re-présenter le plan MIS À JOUR (section 3) et réafficher le menu
- **SI R** : Demander à l'utilisateur des indications sur l'approche à changer (priorité de regroupement différente, granularité différente, etc.). Régénérer le plan depuis zéro avec les nouvelles indications, puis le présenter (section 3) et réafficher le menu
- **SI X** : Afficher "Plan annulé. Aucun commit n'a été effectué." — ARRÊTER le workflow
- **SI Autre** : Expliquer les options disponibles, puis réafficher le menu

#### RÈGLES D'EXÉCUTION :

- TOUJOURS s'arrêter et attendre la saisie utilisateur après avoir présenté le menu
- Ne passer à l'exécution QUE lorsque l'utilisateur sélectionne 'V'
- Après M ou R, TOUJOURS re-présenter le plan complet mis à jour ET le menu
- L'utilisateur peut itérer M ou R plusieurs fois — toujours s'adapter

## MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### SUCCÈS :

- Le plan couvre TOUS les fichiers modifiés sans omission
- Chaque commit est atomique et logiquement cohérent
- Les messages de commit suivent les conventions du projet détectées
- L'ordre respecte toutes les contraintes de dépendance
- L'utilisateur a explicitement validé le plan avec 'V'

### ÉCHEC :

- Fichiers manquants dans le plan
- Commits contenant des changements non liés
- Messages ne suivant pas les conventions détectées
- Ordre des dépendances violé
- L'utilisateur a abandonné le workflow avec 'X'

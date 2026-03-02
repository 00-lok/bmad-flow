---
name: 'step-05-execute'
description: 'Exécuter le plan de commits validé — créer chaque commit dans l''ordre'
---

# Étape 5 : Exécution

## OBJECTIF DE L'ÉTAPE :

Exécuter le plan de commits validé en créant chaque commit dans l'ordre spécifié. Vérifier le succès après chaque commit et présenter un résumé final.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE D'ABORD) :

### Règles Universelles :

- CRITIQUE : Lire le fichier d'étape complet avant toute action

### Règles Spécifiques à l'Étape :

- Exécuter EXACTEMENT le plan validé — ne pas dévier des messages ou regroupements de fichiers approuvés
- Si une commande git échoue, ARRÊTER immédiatement et signaler l'erreur avec la sortie complète
- Vérifier que chaque commit a réussi avant de passer au suivant
- Ne JAMAIS utiliser de flags git destructifs : pas de `--force`, pas de `--amend`, pas de `--no-verify`
- Ne JAMAIS pousser vers le remote — tous les commits restent locaux
- Ne JAMAIS modifier le contenu des fichiers — uniquement stage et commit les changements existants

## SÉQUENCE OBLIGATOIRE

### 1. Vérification de Sécurité Pré-Exécution

Avant toute opération de commit :

- Exécuter `git status --porcelain` et comparer avec l'inventaire de l'étape 03
- **SI l'état de l'arbre de travail a changé** depuis l'analyse (nouveaux fichiers apparus, fichiers modifiés davantage) :
  Afficher : "⚠️ Des changements supplémentaires ont été détectés depuis l'analyse. Il est recommandé de relancer le workflow pour les inclure dans le plan."
  Demander à l'utilisateur : **[P]** Poursuivre quand même | **[X]** Annuler
  - SI P : Continuer avec le plan validé (les nouveaux changements resteront non commités)
  - SI X : ARRÊTER le workflow
- **SI l'arbre de travail correspond** : Poursuivre silencieusement

### 2. Préparer une Zone de Staging Propre

Exécuter `git reset HEAD` une fois pour tout unstage, assurant une base propre pour le staging séquentiel.

SI des fichiers ont été intentionnellement stagés par l'utilisateur, c'est attendu — le workflow les re-stagera dans les regroupements de commits corrects.

### 3. Exécuter Chaque Commit

Pour chaque commit du plan validé (dans l'ordre, commit 1 à N) :

**a) Stager les fichiers :**
- Pour chaque fichier de la liste de ce commit :
  - `git add "<file-path>"` (mettre les chemins entre guillemets pour gérer les espaces)
  - Pour les fichiers supprimés : `git add "<deleted-file-path>"` (git add stage les suppressions)

**b) Vérifier le staging :**
- Exécuter `git diff --cached --name-only`
- Comparer les fichiers stagés avec le plan pour ce commit
- **SI incohérence** : Afficher la discordance et ARRÊTER — ne pas créer le commit

**c) Créer le commit :**
- Message sur une ligne : `git commit -m "<message>"`
- Message avec corps : `git commit -m "<first line>" -m "<body>"`
- Utiliser le message EXACT du plan validé — aucune modification

**d) Vérifier le succès :**
- Vérifier le code de sortie — doit être 0
- **SI le commit a échoué** (rejet du hook pre-commit, erreur GPG, etc.) :
  Afficher la sortie d'erreur complète
  Afficher : "❌ Le commit X/N a échoué. Veuillez résoudre le problème et relancer le workflow."
  ARRÊTER le workflow — ne pas tenter d'autres commits
- **SI succès** :
  Afficher : "✅ Commit X/N créé : `<message>`"

### 4. Vérification Finale

Après création de tous les commits :

- Exécuter `git log --oneline -<N>` (où N = nombre de commits créés) pour afficher les nouveaux commits
- Exécuter `git status` pour afficher l'état final de l'arbre de travail

### 5. Présenter le Résumé Final

Afficher :

---

**🎉 Smart Commit terminé !**

**━━━ Résumé ━━━**
- **Commits créés :** N
- **Fichiers commités :** F
- **Branche :** branch_name

**Commits créés (du plus ancien au plus récent) :**
1. `<short-hash>` — `<message>`
2. `<short-hash>` — `<message>`
...

**État de l'arbre de travail :** propre / X fichiers restants

💡 Les commits sont locaux. Utilisez `git push` quand vous êtes prêt à les publier.

---

## MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### SUCCÈS :

- Les N commits créés avec succès
- Chaque commit contient exactement les fichiers spécifiés dans le plan
- État de l'arbre de travail conforme (propre ou seuls les fichiers non planifiés restent)
- Résumé final affiché avec les hash des commits

### ÉCHEC :

- Une commande git a échoué pendant l'exécution
- Incohérence de staging détectée entre le plan et les fichiers stagés réels
- Le commit a été rejeté par un hook pre-commit
- L'arbre de travail s'est retrouvé dans un état inattendu

**Règle Maîtresse :** Si un commit échoue, ARRÊTER immédiatement. Ne PAS tenter de continuer avec les commits restants — l'utilisateur doit d'abord résoudre le problème.

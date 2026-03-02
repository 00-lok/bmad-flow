---
name: 'step-06-application'
description: 'Appliquer les décisions de documentation en mettant à jour les artefacts BMAD sur place et générer les éléments d\'action pour les corrections de code'

nextStepFile: './step-07-snapshot.md'
checkpointFolder: '{checkpointFolder}'
---

# Étape 6 : Application des Décisions

## OBJECTIF DE L'ÉTAPE :

Appliquer toutes les décisions de mise à jour de documentation en modifiant les artefacts BMAD à leurs emplacements d'origine, vérifier la cohérence post-modification, et compiler toutes les actions correctives sur le code dans un fichier `action-items.md` priorisé.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE EN PREMIER) :

### Règles Universelles :

- 🛑 NE JAMAIS générer de contenu sans entrée utilisateur
- 📖 CRITIQUE : Lire le fichier d'étape complet avant toute action
- 🔄 CRITIQUE : Lors du chargement de l'étape suivante avec 'C', s'assurer que le fichier entier est lu
- 📋 VOUS ÊTES UN FACILITATEUR, pas un générateur de contenu
- ✅ VOUS DEVEZ TOUJOURS PARLER EN SORTIE dans {communication_language}
- ⚙️ REPLI OUTIL/SOUS-PROCESSUS : Si une instruction fait référence à un sous-processus, sous-agent ou outil auquel vous n'avez pas accès, vous DEVEZ malgré tout atteindre le résultat dans votre fil de contexte principal

### Rappel du Rôle :

- ✅ Vous êtes un éditeur de documentation méticuleux et vérificateur de cohérence
- ✅ Précis, méthodique. Chaque modification est exacte et vérifiée.
- ✅ Vous apportez une expertise en maintien de la cohérence documentaire à travers plusieurs artefacts

### Règles Spécifiques à l'Étape :

- 🎯 Appliquer UNIQUEMENT les décisions marquées [D] (mise à jour documentation) de decisions-log.md
- 🚫 INTERDIT de modifier du code — uniquement les artefacts BMAD
- 💬 Pour chaque artefact modifié, vérifier qu'il reste cohérent en interne
- 🚫 INTERDIT de changer les décisions — appliquer exactement ce qui a été décidé à l'étape 05
- 📋 Après toutes les modifications, vérifier la cohérence inter-artefacts

## PROTOCOLES D'EXÉCUTION :

- 🎯 Suivre la SÉQUENCE OBLIGATOIRE exactement
- 💾 Modifier les artefacts sur place à leurs emplacements d'origine
- 💾 Écrire action-items.md dans le dossier checkpoint
- 📖 Mettre à jour stepsCompleted dans checkpoint-summary.md
- 🚫 Ne PAS ignorer aucune décision de mise à jour de documentation

## LIMITES DU CONTEXTE :

- Disponible : decisions-log.md avec toutes les décisions et actions spécifiques
- Focus : Appliquer les mises à jour de documentation, compiler les actions code
- Limites : Modifier uniquement les artefacts pour les décisions [D], NE PAS toucher au code
- Dépendances : étape 05 terminée avec décisions confirmées

## SÉQUENCE OBLIGATOIRE

**CRITIQUE :** Suivre cette séquence exactement. Ne pas sauter, réordonner ou improviser sauf demande explicite de l'utilisateur.

### 1. Charger le Journal des Décisions

Lire `{checkpointFolder}/decisions-log.md` pour obtenir toutes les décisions.

Séparer en deux listes :
- **[D] Mises à jour documentation** — artefacts à modifier
- **[C] Actions correctives code** — éléments pour action-items.md

### 2. Annoncer le Démarrage de l'Application

"**Application des décisions de réalignement.**

**Mises à jour documentation :** [count] artefacts à modifier
**Actions code :** [count] actions à compiler

Le BMad Master applique maintenant les modifications aux artefacts BMAD."

### 3. Appliquer les Mises à Jour de Documentation

Pour chaque décision [D] :

1. **Charger** l'artefact cible à son emplacement d'origine
2. **Appliquer** la modification spécifique documentée dans le journal des décisions
3. **Vérifier** que l'artefact reste cohérent en interne après modification
4. **Sauvegarder** l'artefact modifié sur place
5. **Consigner** ce qui a été changé, où, et le résumé avant/après

Présenter la progression au développeur :
"✅ [Nom de l'artefact] mis à jour — [brève description du changement]"

### 4. Vérification de Cohérence Inter-Artifacts

Après que toutes les mises à jour individuelles soient appliquées :

- Relire tous les artefacts modifiés
- Vérifier que les modifications ne créent pas de NOUVELLES incohérences entre artefacts
- Si de nouvelles incohérences sont trouvées, les signaler au développeur :

"**⚠️ Vérification de cohérence post-modification :**
La modification de [artefact A] crée une possible incohérence avec [artefact B] :
- [Description]

Souhaitez-vous que je corrige également [artefact B] pour maintenir la cohérence ?"

Appliquer les corrections supplémentaires si le développeur accepte.

### 5. Compiler les Éléments d'Action Code

Pour chaque décision [C], compiler dans une liste d'éléments d'action structurée :

Grouper par priorité (critiques en premier) et par zone affectée.

### 6. Rédiger les Éléments d'Action

Créer `{checkpointFolder}/action-items.md` :

```markdown
# Actions Correctives à Planifier

## Date: {date}

## Résumé
- Actions totales: X
- 🔴 Critiques: X
- 🟡 Importantes: X
- 🟢 Mineures: X

## Actions par priorité

### 🔴 Actions critiques

#### [MA-ID] [Titre]
- **Zone du code:** [fichiers/modules spécifiques affectés]
- **Ce qu'il faut faire:** [action corrective spécifique]
- **Pourquoi:** [référence au désalignement d'origine]
- **Effort estimé:** [estimation approximative si possible]

### 🟡 Actions importantes
[Même schéma]

### 🟢 Actions mineures
[Même schéma]

## Suggestions de planification
[Optionnel : regrouper les actions liées en sprints ou lots de travail potentiels]
```

### 7. Rapporter les Résultats de l'Application

"**Application terminée :**

**Artefacts mis à jour ([count]) :**
- ✅ [Lister chaque artefact modifié avec brève description du changement]

**Vérification de cohérence :** [Réussie / Problèmes trouvés et résolus]

**Actions code compilées ([count]) :**
- 🔴 [count] critiques
- 🟡 [count] importantes  
- 🟢 [count] mineures

Le détail des actions est dans `action-items.md`."

### 8. Mettre à Jour le Résumé du Checkpoint

Mettre à jour le frontmatter de `{checkpointFolder}/checkpoint-summary.md` :
- Ajouter `step-06-application` à `stepsCompleted`
- Définir `lastStep: 'step-06-application'`

### 9. Présenter les OPTIONS DU MENU

Afficher : **[C] Continuer — Générer le snapshot final**

#### Logique de Gestion du Menu :

- SI C : Vérifier que action-items.md est écrit, les artefacts sont mis à jour et checkpoint-summary.md est mis à jour, puis charger, lire le fichier entier, puis exécuter {nextStepFile}
- SI Autre : aider l'utilisateur, puis réafficher le menu

#### RÈGLES D'EXÉCUTION :

- TOUJOURS s'arrêter et attendre l'entrée utilisateur après la présentation du menu
- NE procéder à l'étape suivante QUE lorsque l'utilisateur sélectionne 'C'

---

## 🚨 MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### SUCCÈS :

- Chaque décision [D] appliquée au bon artefact
- Artefacts modifiés sur place à leurs emplacements d'origine
- Cohérence post-modification vérifiée
- Nouvelles incohérences signalées et résolues
- action-items.md complet rédigé avec actions code priorisées
- Développeur informé de tous les changements effectués

### ÉCHEC SYSTÈME :

- Ignorer des décisions de mise à jour de documentation
- Modifier le code (ce n'est pas le rôle de cette étape)
- Changer les décisions prises à l'étape 05
- Ne pas vérifier la cohérence post-modification
- Créer de nouvelles incohérences entre artefacts

**Règle Maîtresse :** Appliquer exactement ce qui a été décidé. Vérifier la cohérence après chaque changement. Ignorer des éléments est INTERDIT.

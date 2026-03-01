---
name: 'step-04-diagnostic'
description: 'Comparer l\'analyse du codebase avec la revue des artefacts pour identifier tous les désalignements'

nextStepFile: './step-05-decisions.md'
checkpointFolder: '{checkpointFolder}'
---

# Étape 4 : Diagnostic des Désalignements

## OBJECTIF DE L'ÉTAPE :

Comparer l'analyse du codebase (étape 02) avec la revue des artefacts (étape 03), identifier chaque désalignement entre l'état prévu et l'état réel, les catégoriser, et produire un `misalignment-report.md` complet regroupé par catégorie.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE EN PREMIER) :

### Règles Universelles :

- 🛑 NE JAMAIS générer de contenu sans entrée utilisateur
- 📖 CRITIQUE : Lire le fichier d'étape complet avant toute action
- 🔄 CRITIQUE : Lors du chargement de l'étape suivante avec 'C', s'assurer que le fichier entier est lu
- 📋 VOUS ÊTES UN FACILITATEUR, pas un générateur de contenu
- ✅ VOUS DEVEZ TOUJOURS PARLER EN SORTIE dans {communication_language}
- ⚙️ REPLI OUTIL/SOUS-PROCESSUS : Si une instruction fait référence à un sous-processus, sous-agent ou outil auquel vous n'avez pas accès, vous DEVEZ malgré tout atteindre le résultat dans votre fil de contexte principal

### Rappel du Rôle :

- ✅ Vous êtes un analyste de réconciliation comparant le plan à la réalité
- ✅ Objectif, factuel, exhaustif. Chaque désalignement est documenté sans jugement.
- ✅ Vous apportez une expertise en analyse des écarts et comparaison systématique

### Règles Spécifiques à l'Étape :

- 🎯 Motif Sous-processus 4 : Lancer des comparaisons parallèles par catégorie lorsque possible
- ⚙️ Si sous-processus indisponible, comparer séquentiellement par catégorie
- 🚫 INTERDIT de prendre des décisions sur la résolution des désalignements — c'est l'étape 05
- 💬 Rapporter les constats objectivement — pas encore de recommandations
- 🚫 NE PAS ÊTRE PARESSEUX — comparer chaque aspect systématiquement

## PROTOCOLES D'EXÉCUTION :

- 🎯 Suivre la SÉQUENCE OBLIGATOIRE exactement
- 💾 Écrire le diagnostic complet dans {checkpointFolder}/misalignment-report.md
- 📖 Mettre à jour stepsCompleted dans checkpoint-summary.md
- 🚫 Ne PAS ignorer aucune catégorie de comparaison

## LIMITES DU CONTEXTE :

- Disponible : codebase-analysis.md (étape 02) + artifacts-review.md (étape 03)
- Focus : COMPARAISON entre le code et les artefacts — identifier les écarts
- Limites : Rapporter les désalignements, NE PAS prescrire de solutions
- Dépendances : étapes 02 et 03 terminées

## SÉQUENCE OBLIGATOIRE

**CRITIQUE :** Suivre cette séquence exactement. Ne pas sauter, réordonner ou improviser sauf demande explicite de l'utilisateur.

### 1. Charger les Rapports d'Analyse

Lire les deux rapports du dossier checkpoint :
- `{checkpointFolder}/codebase-analysis.md`
- `{checkpointFolder}/artifacts-review.md`

### 2. Annoncer le Démarrage du Diagnostic

"**Lancement du diagnostic des désalignements.**
Le BMad Master compare le code source avec les artefacts BMAD pour identifier toutes les divergences."

### 3. Comparaison Architecturale

Comparer l'architecture réelle du code avec ce que spécifie le document d'architecture :

- **Structure du projet** : L'organisation des dossiers/fichiers suit-elle l'architecture prévue ?
- **Patterns architecturaux** : Les patterns utilisés dans le code correspondent-ils à ceux documentés ?
- **Composants/Modules** : Tous les composants prévus existent-ils ? Y en a-t-il de non prévus ?
- **Couches et responsabilités** : La séparation des responsabilités est-elle respectée ?
- **Stack technique** : Les technologies utilisées correspondent-elles à celles prévues ?

### 4. Comparaison de la Couverture Fonctionnelle

Comparer les fonctionnalités implémentées avec les exigences du PRD/Stories :

- **Fonctionnalités implémentées** vs **fonctionnalités prévues dans le PRD**
- **Couverture des stories** : Quelles stories sont implémentées, partiellement, ou pas du tout ?
- **Critères d'acceptation** : Les implémentations respectent-elles les critères définis ?
- **Fonctionnalités non prévues** : Y a-t-il du code qui implémente des choses non documentées ?

### 5. Comparaison UX/UI

Si des artefacts de design UX existent, comparer :

- **Composants UI** : Les composants correspondent-ils aux maquettes/wireframes ?
- **Flux utilisateur** : Les parcours implémentés suivent-ils les flux définis ?
- **Design system** : Les conventions visuelles sont-elles respectées ?
- **Responsive/Accessibility** : Conformité avec les exigences UX

### 6. Comparaison des Décisions Techniques

Comparer les choix techniques dans le code vs la documentation :

- **Dépendances** : Les librairies utilisées correspondent-elles à celles prévues ?
- **Patterns de données** : Le modèle de données suit-il le schema prévu ?
- **API design** : Les endpoints/interfaces suivent-ils la spécification ?
- **Configuration** : La configuration suit-elle les pratiques documentées ?

### 7. Catégoriser et Prioriser

Regrouper tous les désalignements identifiés par catégories :

**Catégories de désalignement :**

1. **Architecture** — Divergences structurelles et patterns
2. **Fonctionnel** — Couverture des fonctionnalités vs PRD
3. **UX/UI** — Divergences avec le design prévu
4. **Stack/Technique** — Choix techniques différents de la doc
5. **Documentation** — Artefacts incomplets, obsolètes ou manquants

**Niveaux de sévérité :**
- 🔴 **Critique** — Impact majeur sur le projet, nécessite attention immédiate
- 🟡 **Important** — Divergence significative à adresser
- 🟢 **Mineur** — Divergence légère, faible impact

### 8. Rédiger le Rapport des Désalignements

Créer `{checkpointFolder}/misalignment-report.md` :

```markdown
# Diagnostic des Désalignements

## Date: {date}

## Résumé

- Désalignements totaux identifiés: X
- 🔴 Critiques: X
- 🟡 Importants: X
- 🟢 Mineurs: X

## 1. Architecture
[Pour chaque désalignement dans cette catégorie:]
### [MA-001] [Titre court]
- **Sévérité:** 🔴/🟡/🟢
- **Prévu (doc):** [ce que dit l'artefact]
- **Réel (code):** [ce que le code fait réellement]
- **Impact:** [ce que signifie ce désalignement]

## 2. Fonctionnel
[Même schéma]

## 3. UX/UI
[Même schéma]

## 4. Stack/Technique
[Même schéma]

## 5. Documentation
[Même schéma]

## Alignements confirmés
[Ce qui EST aligné — important pour la confiance]
```

### 9. Mettre à Jour le Résumé du Checkpoint

Mettre à jour le frontmatter de `{checkpointFolder}/checkpoint-summary.md` :
- Ajouter `step-04-diagnostic` à `stepsCompleted`
- Définir `lastStep: 'step-04-diagnostic'`

### 10. Présenter le Résumé du Diagnostic

Présenter l'inventaire complet groupé au développeur :

"**Diagnostic terminé. Voici l'inventaire complet des désalignements :**

**🔴 Critiques ([count]) :**
- [Lister brièvement]

**🟡 Importants ([count]) :**
- [Lister brièvement]

**🟢 Mineurs ([count]) :**
- [Lister brièvement]

**✅ Alignements confirmés :**
- [Domaines clés qui sont alignés]

Le rapport détaillé est dans `misalignment-report.md`. L'étape suivante vous permettra de prendre des décisions sur chaque désalignement."

### 11. Présenter les OPTIONS DU MENU

Afficher : **[C] Continuer — Passer aux décisions de réalignement**

#### Logique de Gestion du Menu :

- SI C : Vérifier que misalignment-report.md est écrit et checkpoint-summary.md est mis à jour, puis charger, lire le fichier entier, puis exécuter {nextStepFile}
- SI Autre : aider l'utilisateur, puis réafficher le menu

#### RÈGLES D'EXÉCUTION :

- TOUJOURS s'arrêter et attendre l'entrée utilisateur après la présentation du menu
- NE procéder à l'étape suivante QUE lorsque l'utilisateur sélectionne 'C'

---

## 🚨 MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### SUCCÈS :

- Les deux rapports d'analyse chargés et croisés
- Chaque catégorie de comparaison couverte systématiquement
- Tous les désalignements identifiés, catégorisés et évalués par sévérité
- Les zones alignées également documentées (pour la confiance)
- misalignment-report.md complet rédigé avec inventaire groupé
- Développeur présenté avec un résumé clair

### ÉCHEC SYSTÈME :

- Catégories de comparaison manquantes
- Faire des recommandations ou décisions (pas encore)
- Ne pas lire les deux rapports d'analyse
- Comparaison superficielle manquant les vrais désalignements
- Ne pas catégoriser ou prioriser les constats

**Règle Maîtresse :** Chaque comparaison doit être approfondie. Le diagnostic doit être complet et objectif. Ignorer des catégories est INTERDIT.

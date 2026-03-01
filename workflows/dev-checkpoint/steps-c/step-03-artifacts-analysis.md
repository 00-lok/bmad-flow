---
name: 'step-03-artifacts-analysis'
description: 'Analyse autonome approfondie de tous les artefacts de planification BMAD existants'

nextStepFile: './step-04-diagnostic.md'
checkpointFolder: '{checkpointFolder}'
---

# Étape 3 : Analyse des Artefacts BMAD

## OBJECTIF DE L'ÉTAPE :

Réaliser une revue autonome et complète de chaque artefact de planification BMAD découvert à l'étape 01 — évaluant le contenu, la complétude, la cohérence interne et la cohérence inter-artefacts de chaque artefact — produisant un rapport détaillé `artifacts-review.md` dans le dossier checkpoint.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE EN PREMIER) :

### Règles Universelles :

- 🛑 JAMAIS générer de contenu sans saisie utilisateur
- 📖 CRITIQUE : Lire le fichier d'étape complet avant toute action
- 🔄 CRITIQUE : Lors du chargement de l'étape suivante avec 'C', s'assurer que le fichier entier est lu
- 📋 VOUS ÊTES UN FACILITATEUR, pas un générateur de contenu
- ✅ VOUS DEVEZ TOUJOURS PARLER EN SORTIE dans {communication_language}
- ⚙️ REPLI OUTIL/SOUS-PROCESSUS : Si une instruction fait référence à un sous-processus, sous-agent ou outil auquel vous n'avez pas accès, vous DEVEZ malgré tout atteindre le résultat dans votre fil de contexte principal

### Rappel du Rôle :

- ✅ Vous êtes un expert analyste méthodologie BMAD et réviseur de documentation
- ✅ Rigoureux, méthodique. Analyse chaque artefact en profondeur.
- ✅ Vous apportez une expertise en structure des artefacts BMAD, critères de complétude et cohérence inter-documents

### Règles Spécifiques à l'Étape :

- 🎯 Analyse approfondie et autonome de chaque artefact BMAD
- 🚫 INTERDIT de comparer avec le code dans cette étape — la comparaison se fait à l'étape 04
- 💬 Pattern Sous-processus 2 : NE PAS ÊTRE PARESSEUX — Pour CHAQUE artefact, lancer un sous-processus pour une analyse approfondie
- ⚙️ Si sous-processus indisponible, analyser chaque artefact séquentiellement dans le fil principal
- 🚫 NE PAS ÊTRE PARESSEUX — lire et analyser chaque artefact complètement

## PROTOCOLES D'EXÉCUTION :

- 🎯 Suivre la SÉQUENCE OBLIGATOIRE exactement
- 💾 Écrire l'analyse complète dans {checkpointFolder}/artifacts-review.md
- 📖 Mettre à jour stepsCompleted dans checkpoint-summary.md
- 🚫 NE PAS sauter d'artefact — la rigueur est critique

## LIMITES DU CONTEXTE :

- Disponible : checkpoint-summary.md avec la liste artifactsDiscovered et les chemins
- Focus : Artefacts BMAD UNIQUEMENT — pas encore de comparaison avec le code
- Limites : Évaluer les artefacts en tant que documents, ne pas comparer au code
- Dépendances : étape 01 (liste des artefacts), étape 02 complétée

## SÉQUENCE OBLIGATOIRE

**CRITIQUE :** Suivre cette séquence exactement. Ne pas sauter, réordonner ou improviser sauf si l'utilisateur demande explicitement un changement.

### 1. Annoncer le Démarrage de l'Analyse

"**Lancement de l'analyse des artefacts BMAD.**
Le BMad Master va lire et analyser chaque document de planification détecté."

### 2. Charger la Liste des Artefacts

Lire `{checkpointFolder}/checkpoint-summary.md` pour obtenir la liste `artifactsDiscovered` avec les chemins des fichiers.

### 3. Analyser Chaque Artefact

NE PAS ÊTRE PARESSEUX — Pour CHAQUE artefact de la liste découverte, lancer un sous-processus (ou analyser séquentiellement si indisponible) qui :

1. Charge et lit l'artefact complet
2. Analyse :
   - **Complétude** : Toutes les sections attendues sont-elles présentes et remplies ?
   - **Clarté** : Les descriptions sont-elles claires, non ambiguës ?
   - **Cohérence interne** : Les informations au sein du document sont-elles cohérentes ?
   - **Niveau de détail** : Le document est-il suffisamment détaillé pour guider le développement ?
   - **Qualité des décisions** : Les choix documentés sont-ils justifiés ?
   - **Maturité** : Le document semble-t-il finalisé ou en brouillon ?
3. Retourne des constats structurés par artefact

**Pour chaque type d'artefact, évaluer les critères spécifiques :**

**Product Brief :**
- Clarté de l'énoncé du problème, audience cible, proposition de valeur, périmètre

**PRD :**
- Complétude des exigences fonctionnelles, user stories, critères d'acceptation, NFRs, métriques de succès

**Architecture :**
- Décisions de stack technique, structure des composants, modèle de données, conception API, sécurité, déploiement, scalabilité

**UX Design :**
- Parcours utilisateur, références wireframes/maquettes, design system, accessibilité, design responsive

**Epics & Stories :**
- Couverture des exigences du PRD, critères d'acceptation, dépendances, estimation, priorité

**Project Context :**
- Exactitude, complétude, informations à jour

### 4. Vérification de la Cohérence Inter-Artefacts

Après avoir analysé chaque artefact individuellement, évaluer la cohérence ENTRE les artefacts :

- Les exigences du PRD sont-elles alignées avec la vision du Product Brief ?
- L'Architecture supporte-t-elle toutes les exigences fonctionnelles du PRD ?
- Les Stories couvrent-elles toutes les exigences du PRD ?
- Le UX Design est-il aligné avec les attentes d'expérience utilisateur du PRD ?
- Y a-t-il des contradictions entre deux artefacts ?
- Les conventions de nommage sont-elles cohérentes entre les artefacts ?

### 5. Rédiger le Rapport de Revue des Artefacts

Créer `{checkpointFolder}/artifacts-review.md` avec le format semi-structuré suivant :

```markdown
# Revue des Artefacts BMAD

## Date: {date}

## Artefacts analysés
[List of all artifacts with paths and dates]

## Analyse par artefact

### [Artifact Name]
- **Complétude:** [score/assessment]
- **Clarté:** [assessment]
- **Cohérence interne:** [assessment]
- **Niveau de détail:** [assessment]
- **Points forts:** [list]
- **Lacunes identifiées:** [list]
- **Recommandations:** [list]

[Repeat for each artifact]

## Cohérence inter-artefacts
- **Alignements confirmés:** [what's consistent]
- **Incohérences détectées:** [contradictions or gaps between artifacts]
- **Artefacts manquants:** [recommended artifacts that don't exist yet]

## Métriques clés
- Nombre d'artefacts analysés: X
- Score de complétude moyen: X
- Incohérences inter-artefacts: X
- Artefacts manquants recommandés: X
```

### 6. Mettre à Jour la Synthèse du Checkpoint

Mettre à jour le frontmatter de `{checkpointFolder}/checkpoint-summary.md` :
- Ajouter `step-03-artifacts-analysis` à `stepsCompleted`
- Définir `lastStep: 'step-03-artifacts-analysis'`

### 7. Présenter le Résumé des Résultats

"**Analyse des artefacts BMAD terminée. Voici les points clés :**
- [Nombre] artefacts analysés
- [Constats clés de cohérence]
- [Lacunes ou problèmes les plus significatifs]

Le rapport complet est dans `artifacts-review.md`. Prêt pour le diagnostic des désalignements."

### 8. Présenter les OPTIONS DU MENU

Afficher : **[C] Continuer — Lancer le diagnostic des désalignements**

#### Logique de Gestion du Menu :

- SI C : Vérifier que artifacts-review.md est écrit et checkpoint-summary.md est mis à jour, puis charger, lire le fichier entier, puis exécuter {nextStepFile}
- SI Autre : aider l'utilisateur, puis réafficher le menu

#### RÈGLES D'EXÉCUTION :

- TOUJOURS s'arrêter et attendre la saisie utilisateur après présentation du menu
- NE passer à l'étape suivante QUE lorsque l'utilisateur sélectionne 'C'

---

## 🚨 MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### ✅ SUCCÈS :

- Chaque artefact découvert entièrement lu et analysé
- Complétude, clarté, cohérence évaluées par artefact
- Cohérence inter-artefacts vérifiée
- Rapport artifacts-review.md complet écrit dans le dossier checkpoint
- stepsCompleted mis à jour dans checkpoint-summary.md

### ❌ ÉCHEC DU SYSTÈME :

- Sauter un artefact de la liste découverte
- Analyse superficielle sans lire les artefacts complets
- Comparer avec le code (pas encore — étape 04)
- Ne pas évaluer la cohérence inter-artefacts
- Ne pas rédiger le rapport complet

**Règle Maîtresse :** Chaque artefact doit être lu complètement et analysé en profondeur. Sauter ou faire une revue superficielle est INTERDIT.

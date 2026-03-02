---
name: 'step-05-decisions'
description: 'Réviser collaborativement les désalignements et prendre les décisions de réalignement avec le développeur'

nextStepFile: './step-06-application.md'
checkpointFolder: '{checkpointFolder}'
advancedElicitationTask: '{project-root}/_bmad/core/workflows/advanced-elicitation/workflow.xml'
partyModeWorkflow: '{project-root}/_bmad/core/workflows/party-mode/workflow.md'
---

# Étape 5 : Décisions de Réalignement

## OBJECTIF DE L'ÉTAPE :

Réviser collaborativement chaque désalignement identifié à l'étape 04 avec le développeur, discuter de chacun, et prendre des décisions claires : mettre à jour la documentation pour correspondre à la réalité OU enregistrer une action corrective sur le code. Chaque décision est justifiée et enregistrée dans `decisions-log.md`.

## RÈGLES D'EXÉCUTION OBLIGATOIRES (LIRE EN PREMIER) :

### Règles Universelles :

- 🛑 NE JAMAIS générer de contenu sans entrée utilisateur
- 📖 CRITIQUE : Lire le fichier d'étape complet avant toute action
- 🔄 CRITIQUE : Lors du chargement de l'étape suivante avec 'C', s'assurer que le fichier entier est lu
- 📋 VOUS ÊTES UN FACILITATEUR, pas un générateur de contenu
- ✅ VOUS DEVEZ TOUJOURS PARLER EN SORTIE dans {communication_language}

### Rappel du Rôle :

- ✅ Vous êtes un conseiller technique aidant le développeur à prendre des décisions éclairées
- ✅ Patient, clair, structuré. Présente les options sans imposer.
- ✅ Vous apportez la perspective technique, le développeur apporte l'autorité métier
- ✅ Le développeur a l'AUTORITÉ FINALE sur chaque désalignement

### Règles Spécifiques à l'Étape :

- 🎯 C'est l'étape COLLABORATIVE — chaque décision nécessite l'entrée du développeur
- 🚫 INTERDIT de prendre des décisions sans confirmation du développeur
- 💬 Présenter les désalignements groupés par catégorie, discuter de chaque groupe
- 📋 Pour chaque désalignement, présenter exactement deux options : mettre à jour la doc OU action sur le code
- 🚫 INTERDIT d'ignorer un désalignement — chacun nécessite une décision

## PROTOCOLES D'EXÉCUTION :

- 🎯 Suivre la SÉQUENCE OBLIGATOIRE exactement
- 💾 Écrire toutes les décisions dans {checkpointFolder}/decisions-log.md
- 📖 Mettre à jour stepsCompleted dans checkpoint-summary.md
- 🚫 NE PAS appliquer de changements pour l'instant — c'est l'étape 06

## LIMITES DU CONTEXTE :

- Disponible : misalignment-report.md (étape 04) avec tous les désalignements catégorisés
- Focus : Prise de décision AVEC le développeur
- Limites : Décider uniquement, NE PAS appliquer de changements pour l'instant
- Dépendances : étape 04 terminée avec rapport de désalignements complet

## SÉQUENCE OBLIGATOIRE

**CRITIQUE :** Suivre cette séquence exactement. Ne pas sauter, réordonner ou improviser sauf demande explicite de l'utilisateur.

### 1. Charger le Rapport des Désalignements

Lire `{checkpointFolder}/misalignment-report.md` pour obtenir l'inventaire complet.

### 2. Présenter le Cadre de Décision

"**Phase de décisions de réalignement.**

Pour chaque désalignement, vous avez deux options :

**[D] Mettre à jour la Documentation** — Le code reflète la bonne réalité. On met à jour l'artefact BMAD pour correspondre.

**[C] Action Corrective sur le Code** — La documentation reflète la bonne intention. On note une action à faire sur le code.

On va procéder catégorie par catégorie, en commençant par les critiques."

### 3. Traiter les Désalignements Critiques en Premier

Présenter tous les désalignements 🔴 Critiques :

Pour chacun :
"**[ID] [Titre]** 🔴 Critique

- **Prévu (doc) :** [ce que dit l'artefact]
- **Réel (code) :** [ce que le code fait réellement]
- **Impact :** [conséquence de ce désalignement]

**Votre décision :**
- **[D]** Mettre à jour la doc (le code est correct)
- **[C]** Action corrective sur le code (la doc est correcte)

Justification ou commentaire ?"

Attendre la réponse du développeur sur chaque élément critique.

### 4. Traiter les Désalignements Importants

Présenter tous les désalignements 🟡 Importants par catégorie.

Pour l'efficacité, les présenter par groupes de 2-3 lorsqu'ils sont liés :

"**Catégorie : [Nom de la catégorie]**

[ID-1] [Titre] — Prévu: [X] / Réel: [Y]
[ID-2] [Titre] — Prévu: [X] / Réel: [Y]

Pour chacun : **[D]** mettre à jour la doc ou **[C]** action sur le code ?"

### 5. Traiter les Désalignements Mineurs

Présenter les désalignements 🟢 Mineurs en lot :

"**Désalignements mineurs :**

| ID | Titre | Prévu | Réel |
|----|-------|-------|------|
| [ID] | [title] | [planned] | [actual] |
| ... | ... | ... | ... |

Le BMad Master recommande **[D] mettre à jour la doc** pour tous les mineurs, sauf si vous préférez autrement. D'accord, ou souhaitez-vous ajuster certains ?"

### 6. Confirmer Toutes les Décisions

"**Récapitulatif de toutes les décisions :**

**Mises à jour de documentation ([count]) :**
- [Lister les ID et titres]

**Actions correctives sur le code ([count]) :**
- [Lister les ID et titres]

Est-ce que ce récapitulatif est correct ? Des changements à apporter ?"

### 7. Rédiger le Journal des Décisions

Créer `{checkpointFolder}/decisions-log.md` :

```markdown
# Journal des Décisions de Réalignement

## Date: {date}
## Décideur: {user_name}

## Résumé
- Désalignements traités: X
- Mises à jour documentation: X
- Actions correctives code: X

## Décisions détaillées

### [MA-001] [Titre]
- **Sévérité:** 🔴/🟡/🟢
- **Décision:** [D] Mettre à jour la documentation / [C] Action corrective code
- **Justification:** [Raisonnement du développeur]
- **Artefact concerné:** [quel artefact BMAD mettre à jour, ou quelle zone de code corriger]
- **Action spécifique:** [ce qui doit exactement changer]

[Répéter pour chaque désalignement]

## Actions correctives à planifier
[Liste de toutes les actions côté code pour référence à l'étape 06]
```

### 8. Mettre à Jour le Résumé du Checkpoint

Mettre à jour le frontmatter de `{checkpointFolder}/checkpoint-summary.md` :
- Ajouter `step-05-decisions` à `stepsCompleted`
- Définir `lastStep: 'step-05-decisions'`

### 9. Présenter les OPTIONS DU MENU

Afficher : **Sélectionnez une option :** [A] Élicitation avancée [P] Party Mode [C] Continuer — Appliquer les décisions

#### Logique de Gestion du Menu :

- SI A : Exécuter {advancedElicitationTask}, et à la fin réafficher le menu
- SI P : Exécuter {partyModeWorkflow}, et à la fin réafficher le menu
- SI C : Vérifier que decisions-log.md est écrit et checkpoint-summary.md est mis à jour, puis charger, lire le fichier entier, puis exécuter {nextStepFile}
- SI Autre : aider l'utilisateur, puis réafficher le menu

#### RÈGLES D'EXÉCUTION :

- TOUJOURS s'arrêter et attendre l'entrée utilisateur après la présentation du menu
- NE procéder à l'étape suivante QUE lorsque l'utilisateur sélectionne 'C'
- Après exécution des autres options du menu, revenir à ce menu

---

## 🚨 MÉTRIQUES DE SUCCÈS/ÉCHEC DU SYSTÈME

### SUCCÈS :

- Chaque désalignement du rapport a reçu une décision
- Le développeur a confirmé toutes les décisions
- Journal des décisions rédigé avec justifications
- Éléments critiques traités en premier
- Traitement par lot utilisé pour les éléments mineurs (efficace)
- Le développeur se sent écouté et en contrôle

### ÉCHEC SYSTÈME :

- Ignorer des désalignements sans décision
- Prendre des décisions sans entrée du développeur
- Appliquer des changements (pas encore — étape 06)
- Ne pas documenter les justifications
- Traiter dans le mauvais ordre (mineurs avant critiques)

**Règle Maîtresse :** Chaque désalignement nécessite une décision. Le développeur a l'autorité finale. Ignorer des éléments est INTERDIT.

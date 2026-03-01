---
name: Dev Checkpoint
description: Workflow de réconciliation et réalignement du contexte projet BMAD avec la réalité du code source
web_bundle: true
---

# Dev Checkpoint

**Goal:** Faire un état des lieux complet du développement, identifier les désalignements entre le contexte BMAD planifié et la réalité du code, prendre des décisions de réalignement, et appliquer concrètement les mises à jour pour que les artefacts BMAD redeviennent une source de vérité fiable.

**Votre Rôle :** En plus de votre nom, communication_style et persona, vous êtes également un analyste technique et architecte logiciel spécialisé BMAD collaborant avec le développeur du projet. C'est un partenariat, pas une relation client-fournisseur. Vous apportez une expertise approfondie en analyse de code, revue d'architecture et gestion des artefacts BMAD, tandis que l'utilisateur apporte sa connaissance du domaine, le contexte de développement et l'autorité décisionnelle. Travaillez ensemble sur un pied d'égalité.

---

## ARCHITECTURE DU WORKFLOW

### Principes Fondamentaux

- **Conception Micro-fichier** : Chaque étape de l'objectif global est un fichier d'instructions autonome auquel vous adhérerez, 1 fichier à la fois comme indiqué
- **Chargement Juste-à-Temps** : Un seul fichier d'étape courant sera chargé, lu et exécuté jusqu'à complétion — ne jamais charger les fichiers d'étapes futures avant d'y être invité
- **Application Séquentielle** : La séquence dans les fichiers d'étapes doit être complétée dans l'ordre, aucun saut ni optimisation autorisé
- **Suivi d'État** : Documenter la progression dans le frontmatter du fichier de sortie en utilisant le tableau `stepsCompleted`
- **Construction par Append** : Construire les documents en ajoutant du contenu comme indiqué au fichier de sortie
- **Optimisation des Sous-processus** : Utiliser les sous-agents pour l'analyse parallèle lorsque disponible, avec repli gracieux vers le traitement séquentiel

### Règles de Traitement des Étapes

1. **LIRE EN ENTIER** : Toujours lire le fichier d'étape complet avant toute action
2. **SUIVRE LA SÉQUENCE** : Exécuter toutes les sections numérotées dans l'ordre, ne jamais dévier
3. **ATTENDRE LA SAISIE** : Si un menu est présenté, s'arrêter et attendre la sélection de l'utilisateur
4. **VÉRIFIER LA CONTINUATION** : Si l'étape a un menu avec Continuer comme option, ne passer à l'étape suivante que lorsque l'utilisateur sélectionne 'C' (Continuer)
5. **SAUVEGARDER L'ÉTAT** : Mettre à jour `stepsCompleted` dans le frontmatter avant de charger l'étape suivante
6. **CHARGER LA SUIVANTE** : Lorsque demandé, charger, lire le fichier entier, puis exécuter le fichier de l'étape suivante

### Règles Critiques (AUCUNE EXCEPTION)

- 🛑 **JAMAIS** charger plusieurs fichiers d'étapes simultanément
- 📖 **TOUJOURS** lire le fichier d'étape entier avant exécution
- 🚫 **JAMAIS** sauter d'étapes ou optimiser la séquence
- 💾 **TOUJOURS** mettre à jour le frontmatter des fichiers de sortie lors de l'écriture de la sortie finale pour une étape spécifique
- 🎯 **TOUJOURS** suivre les instructions exactes du fichier d'étape
- ⏸️ **TOUJOURS** s'arrêter aux menus et attendre la saisie de l'utilisateur
- 📋 **JAMAIS** créer de listes mentales de tâches à partir des étapes futures
- ⚙️ **REPLI OUTIL/SOUS-PROCESSUS** : Si une instruction fait référence à un sous-processus, sous-agent ou outil auquel vous n'avez pas accès, vous DEVEZ malgré tout atteindre le résultat dans votre fil de contexte principal

---

## SÉQUENCE D'INITIALISATION

### 1. Chargement de la Configuration du Module

Charger et lire la configuration complète depuis {project-root}/_bmad/bmm/config.yaml et résoudre :

- `project_name`, `output_folder`, `user_name`, `communication_language`, `document_output_language`, `planning_artifacts`

### 2. EXÉCUTION de la Première Étape

Charger, lire le fichier complet puis exécuter `./steps-c/step-01-init.md` pour commencer le workflow.

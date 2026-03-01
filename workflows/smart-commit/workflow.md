---
name: Smart Commit
description: Analyse le contexte projet et les changements non commités pour créer un plan de commits intelligent respectant les conventions du projet, puis exécute les commits après validation
web_bundle: true
---

# Smart Commit

**Objectif :** Analyser en profondeur le contexte du projet et l'ensemble des changements non commités, élaborer un plan de commits logique et propre respectant les conventions du projet, puis exécuter les commits après validation de l'utilisateur.

**Votre Rôle :** En plus de votre nom, communication_style et persona, vous êtes un expert Git et en bonnes pratiques de versionnement collaborant avec le développeur du projet. Il s'agit d'un partenariat, pas d'une relation client-fournisseur. Vous apportez une expertise approfondie en workflows Git, conventions de commit et organisation du code, tandis que l'utilisateur apporte sa connaissance du domaine et le contexte de développement. Travaillez ensemble en tant qu'égaux.

**Méta-Contexte :** Ce workflow automatise le travail cognitif de planification de commits propres et atomiques. Il analyse le contexte complet du projet, détecte les conventions existantes et génère un plan de commits optimal — l'utilisateur n'a qu'à valider le plan avant l'exécution.

---

## ARCHITECTURE DU WORKFLOW

Ce workflow utilise une **architecture par fichiers d'étapes** pour une exécution disciplinée :

### Principes Fondamentaux

- **Conception Micro-fichier** : Chaque étape est un fichier d'instructions autonome qui doit être suivi exactement
- **Chargement Juste-à-temps** : Seul le fichier de l'étape courante est en mémoire — ne jamais charger les fichiers d'étapes futures avant d'y être invité
- **Application Séquentielle** : La séquence définie dans les fichiers d'étapes doit être complétée dans l'ordre, sans saut ni optimisation autorisée
- **Optimisation des Sous-processus** : Utiliser des sous-agents pour l'analyse parallèle lorsque disponible, avec repli gracieux vers un traitement séquentiel

### Règles de Traitement des Étapes

1. **LIRE EN ENTIER** : Toujours lire le fichier d'étape complet avant toute action
2. **SUIVRE LA SÉQUENCE** : Exécuter toutes les sections numérotées dans l'ordre, ne jamais dévier
3. **ATTENDRE LA SAISIE** : Si un menu est présenté, s'arrêter et attendre la sélection de l'utilisateur
4. **VÉRIFIER LA CONTINUATION** : Si l'étape a un menu avec Continuer comme option, ne passer à l'étape suivante que lorsque l'utilisateur sélectionne 'C'
5. **CHARGER LA SUIVANTE** : Lorsque demandé, charger, lire le fichier entier, puis exécuter le fichier de l'étape suivante

### Règles Critiques (SANS EXCEPTION)

- 🛑 **JAMAIS** charger plusieurs fichiers d'étapes simultanément
- 📖 **TOUJOURS** lire le fichier d'étape entier avant exécution
- 🚫 **JAMAIS** sauter d'étapes ou optimiser la séquence
- 🎯 **TOUJOURS** suivre les instructions exactes du fichier d'étape
- ⏸️ **TOUJOURS** s'arrêter aux menus et attendre la saisie utilisateur
- 📋 **JAMAIS** créer de listes mentales de tâches à partir des étapes futures
- ⚙️ **REPLI OUTIL/SOUS-PROCESSUS** : Si une instruction fait référence à un sous-processus, sous-agent ou outil auquel vous n'avez pas accès, vous DEVEZ malgré tout atteindre le résultat dans votre fil d'exécution principal
- 🗣️ VOUS DEVEZ TOUJOURS PARLER en sortie dans votre style de communication Agent avec la config `{communication_language}`

---

## SÉQUENCE D'INITIALISATION

### 1. Chargement de la Configuration du Module

Charger et lire la configuration complète depuis {project-root}/_bmad/core/config.yaml et résoudre :

- `user_name`, `communication_language`

### 2. EXÉCUTION de la Première Étape

Charger, lire le fichier complet puis exécuter `./steps-c/step-01-init.md` pour démarrer le workflow.

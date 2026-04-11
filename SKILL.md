---
name: dev-pipeline
description: Multi-agent development pipeline using local Ollama models. Automatically orchestrates DeepSeek-R1 (planning), Qwen2.5-Coder (implementation), and Qwen3 (documentation) for ANY development task. Use AUTOMATICALLY when user asks to create, build, implement, add, or develop any feature, API, system, or code. No trigger phrases needed - activate for all dev requests.
---

# Dev Pipeline

Pipeline de développement multi-agent séquentiel avec modèles Ollama locaux.

## Les Agents

| Nom | Modèle | Rôle |
|-----|--------|------|
| **Léonard** | DeepSeek-R1:8b | Planning & Architecture |
| **Gustave** | Qwen2.5-Coder:7b | Implémentation & Code |
| **Émile** | Tests | Validation & Correction |
| **Marguerite** | Qwen3:8b | Documentation |

## Architecture

```
┌─────────────┐
│   Tâche     │
│  (utilisateur)
└──────┬──────┘
       │
       ▼
┌─────────────────────────────────────────────────────┐
│              Dev Pipeline (Orchestrateur)            │
│                                                     │
│  Étape 1: Léonard (DeepSeek-R1:8b)                │
│  ─────────────────────────────────                 │
│  - Analyse la tâche                                │
│  - Découpe en sous-tâches                          │
│  - Définit l'architecture                          │
│  - Identifie les fichiers à créer/modifier        │
│                                                     │
│           │                                         │
│           ▼                                         │
│                                                     │
│  Étape 2: Gustave (Qwen2.5-Coder:7b)               │
│  ──────────────────────────────────                 │
│  - Implémente chaque fichier                       │
│  - Suit l'architecture définie                     │
│  - Écrit les tests unitaires                       │
│                                                     │
│           │                                         │
│           ▼                                         │
│                                                     │
│  Étape 3: Émile (Tests)                            │
│  ─────────────────────                             │
│  - Lance les tests (pnpm test, pytest, etc.)       │
│  - Rapporte les échecs                             │
│  - Demande corrections si nécessaire               │
│                                                     │
│           │                                         │
│           ▼                                         │
│                                                     │
│  Étape 4: Marguerite (Qwen3:8b)                   │
│  ────────────────────────────────                   │
│  - Génère README.md                                │
│  - Génère TESTING.md                               │
│  - Génère ARCHITECTURE.md                         │
│  - Met à jour MEMORY.md si applicable             │
│                                                     │
└─────────────────────────────────────────────────────┘
```

## Usage

**AUTOMATIQUE** - Pas de phrases magiques.

Le pipeline se déclenche automatiquement pour **TOUTE** tâche impliquant du code :

```
"Crée une API REST"
"Ajoute un bouton"
"Modifie le CSS"
"Corrige un bug"
"Refactor ce fichier"
"Change la couleur du header"
```

**Règle OBLIGATOIRE** : Si ça touche à du code, ça passe par le Pipeline.

### ✅ Pipeline obligatoire
- Créer/modifier/supprimer du code
- Modifier un fichier source (.ts, .tsx, .js, .py, .swift, etc.)
- Changer du CSS, HTML, config
- Ajouter une feature, un composant, une fonction
- Corriger un bug, refactor
- Tests, documentation technique

### ❌ Pas de Pipeline
- Lire un fichier
- Répondre au chat
- Lancer une commande système
- Rechercher sur le web
- Gérer des rappels/notes

**Détection automatique**:
- Verbes: créer, ajouter, implémenter, développer, coder, builder, modifier, changer, corriger, refactor, supprimer
- Sujets: API, feature, système, module, service, component, fichier, code, fonction, bug, CSS, style
- Pas besoin de dire "pipeline" ou "avec le pipeline"

Le skill détecte que c'est du dev et lance automatiquement les 4 étapes.

## Prérequis

1. **Modèles Ollama installés**:
   - `deepseek-r1:8b` — Planning & reasoning
   - `qwen2.5-coder:7b` — Code implementation
   - `qwen3:8b` — Documentation

2. **Environnement de développement**:
   - Node.js / Python selon le projet
   - Tests configurés (Vitest, Jest, pytest, etc.)

## Workflow Détaillé

### Étape 1: Analyse (Léonard)

**🔔 DÉBUT**:
```
🔄 Léonard prend le relais pour l'analyse et la planification...
```

**🔔 SOUS-ÉTAPES** (notifier à chaque) :

1. **Lecture du contexte**:
```
📖 Léonard lit le contexte du projet...
```

2. **Compréhension du besoin**:
```
🧠 Léonard analyse la demande...
💭 Compréhension: [résumé en 1 phrase]
```

3. **Architecture**:
```
🏗️ Léonard conçoit l'architecture...
📐 Composants: [liste]
```

4. **Identification des fichiers**:
```
📁 Léonard identifie les fichiers à créer/modifier...
├── src/index.ts — Entry point
├── src/routes/api.ts — API endpoints
└── tests/api.test.ts — Tests unitaires
```

5. **Dépendances**:
```
📦 Léonard identifie les dépendances...
- express@4.18.2
- typescript@5.0.0
```

6. **Risques**:
```
⚠️ Léonard identifie les risques...
- [risque 1]
- [risque 2]
```

**🔔 FIN**:
```
✅ Léonard a terminé l'analyse.
📋 Plan complet généré.

🔧 Gustave prend le relais pour l'implémentation...
```

---

### Étape 2: Implémentation (Gustave)

**🔔 DÉBUT**:
```
🔧 Gustave prend le relais pour l'implémentation...
📋 Fichiers à créer: [N] fichiers
```

**🔔 SOUS-ÉTAPES** (notifier pour CHAQUE fichier) :

Pour chaque fichier:

1. **Début du fichier**:
```
📝 Gustave travaille sur: [filename]
📄 Rôle: [description du rôle]
```

2. **Génération** (si fichier long) :
```
⏳ Gustave génère le code... (peut prendre 30-60s)
```

3. **Écriture**:
```
💾 Fichier écrit: [filename]
📊 Taille: [X lignes]
```

4. **Progression**:
```
📈 Progression: [X/N] fichiers
```

**🔔 FIN**:
```
✅ Gustave a terminé l'implémentation.
📁 Fichiers créés: [N] fichiers
📊 Total: [X lignes de code]

🧪 Émile prend le relais pour la validation...
```

---

### Étape 3: Validation (Émile)

**🔔 DÉBUT**:
```
🧪 Émile prend le relais pour la validation...
📋 Tests à exécuter: [framework]
```

**🔔 SOUS-ÉTAPES** (notifier à chaque) :

1. **Lancement des tests**:
```
🚀 Émile lance les tests...
⏳ Commande: [pnpm test / pytest / etc.]
```

2. **Exécution** (pendant les tests) :
```
⏳ Tests en cours... (peut prendre 10-30s)
```

3. **Résultats**:
```
📊 Résultats:
✅ Passés: [X]
❌ Échoués: [Y]
⏭️ Ignorés: [Z]
```

4. **Coverage**:
```
📈 Coverage: [X%]
```

**🔔 FIN** (succès) :
```
✅ Émile a validé le code.
🎉 Tous les tests passent !

📚 Marguerite prend le relais pour la documentation...
```

**🔔 FIN** (échec) :
```
⚠️ Émile a détecté des erreurs.

❌ Tests échoués:
[Test 1]: [erreur]
[Test 2]: [erreur]

🔧 Gustave corrige les erreurs...
```

**Corrections** (si échec) :
```
🔧 Gustave analyse l'erreur: [test name]
🔍 Cause: [raison]
🛠️ Correction appliquée

🧪 Émile relance les tests...
```

---

### Étape 4: Documentation (Marguerite)

**🔔 DÉBUT**:
```
📚 Marguerite prend le relais pour la documentation...
📄 Documents à générer: README.md, TESTING.md, ARCHITECTURE.md
```

**🔔 SOUS-ÉTAPES** (notifier pour CHAQUE document) :

1. **README.md**:
```
📝 Marguerite rédige README.md...
⏳ Génération en cours...
💾 README.md écrit
```

2. **TESTING.md**:
```
📝 Marguerite rédige TESTING.md...
⏳ Génération en cours...
💾 TESTING.md écrit
```

3. **ARCHITECTURE.md**:
```
📝 Marguerite rédige ARCHITECTURE.md...
⏳ Génération en cours...
💾 ARCHITECTURE.md écrit
```

4. **MEMORY.md** (si applicable) :
```
📝 Marguerite met à jour MEMORY.md...
💾 MEMORY.md mis à jour
```

**🔔 FIN**:
```
✅ Marguerite a terminé la documentation.
📄 Fichiers générés: README.md, TESTING.md, ARCHITECTURE.md

🎉 ========================================
🎉 PIPELINE TERMINÉ !
🎉 ========================================

📋 Résumé:
├── Analyse (Léonard): [X fichiers identifiés]
├── Implémentation (Gustave): [Y lignes de code]
├── Validation (Émile): [Z tests passés]
└── Documentation (Marguerite): [N fichiers générés]

⏱️ Temps total: [temps]
📊 Qualité: [score estimé]
```

---

## Commandes Ollama

```bash
# Vérifier les modèles installés
ollama list

# Lancer un modèle en interactif
ollama run deepseek-r1:8b    # Bernard
ollama run qwen2.5-coder:7b # Marcel
ollama run qwen3:8b         # Colette
```

## Gestion d'Erreurs

| Erreur | Action | Agent |
|--------|--------|-------|
| Plan flou | Re-prompt avec plus de contexte | Léonard |
| Code incomplet | Continuer le code | Gustave |
| Tests échouent | Corriger le code | Gustave |
| Doc incomplète | Re-prompt avec limites | Marguerite |

## Templates de Prompts

Voir `references/prompts.md` pour les templates détaillés par étape.

## Exemples Complets

Voir `references/examples.md` pour des exemples concrets d'exécution.

## Notes importantes

- **Séquentiel**: Un seul modèle à la fois (contrainte RAM 16GB)
- **Notifications DÉTAILLÉES**: À chaque sous-étape, informer Ed
- **Pas de rush**: Les agents prennent leur temps pour la qualité
- **Temps = Qualité**: Mieux vaut lent et bien que rapide et bâclé
- **NOMMER EXPLICITEMENT**: TOUJOURS utiliser le nom de l'agent, jamais "je" ou "j'ai"
- **Thierry = Orchestrateur**: Quand Thierry agit seul, dire "Thierry a..."
- **Contexte préservé**: Chaque étape reçoit le output de la précédente
- **Itératif**: Les échecs peuvent revenir à l'étape précédente
- **Documenté**: Tout est tracé dans MEMORY.md ou le projet
- **Feedback constant**: Ed est informé en temps réel de tout ce qui se passe

## Règle de nommage

**OBLIGATOIRE** — Nommer explicitement l'agent dans TOUTES les communications :

| Qui | Action | Formulation |
|-----|--------|-------------|
| Thierry | Lit un fichier | "Thierry a lu config.json" |
| Thierry | Répond au chat | "Thierry répond: ..." |
| Léonard | Analyse | "Léonard a analysé la demande" |
| Gustave | Code | "Gustave a implémenté UserCard" |
| Émile | Teste | "Émile a exécuté 15 tests" |
| Marguerite | Documente | "Marguerite a rédigé README.md" |

**INTERDIT**: "J'ai fait", "Je vais", "J'ai créé"
**OBLIGATOIRE**: "Thierry a fait", "Léonard a analysé", "Gustave a créé"
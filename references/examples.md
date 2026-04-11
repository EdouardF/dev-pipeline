# Exemples Concrets d'Usage du Pipeline

## Exemple 1: API REST Todos

### Commande utilisateur
```
"Crée une API REST pour gérer des todos avec le pipeline"
```

### Étape 1: Analyse (DeepSeek-R1)

**Prompt envoyé**:
```
Tu es un architecte logiciel senior. Analyse cette tâche et fournis un plan structuré.

Tâche: Créer une API REST pour gérer des todos avec authentification JWT

Contexte du projet:
- Node.js + Express + TypeScript
- Base de données: SQLite (fichier)
- Tests: Vitest
```

**Output**:
- Compréhension: API REST CRUD pour todos avec auth JWT
- Fichiers: `src/index.ts`, `src/db/init.ts`, `src/middleware/auth.ts`, `src/routes/todos.ts`, `src/types/todo.ts`, `tests/todos.test.ts`
- Dépendances: `express`, `jsonwebtoken`, `better-sqlite3`

### Étape 2: Implémentation (Qwen2.5-Coder)

Fichiers créés séquentiellement avec tests unitaires inclus.

### Étape 3: Validation

```bash
pnpm test
# Tests: 12 passed, Coverage: 87%
```

### Étape 4: Documentation (Qwen3)

README.md, TESTING.md, ARCHITECTURE.md générés.

---

## Exemple 2: Système de Cache Redis

### Commande
```
"Dev pipeline: implémente un système de cache Redis avec TTL configurable"
```

### Résultat
- Fichiers: 4 créés
- Tests: 15 passés
- Coverage: 92%

---

## Patterns Récurrents

| Type de projet | Fichiers typiques |
|----------------|-------------------|
| API REST | `index.ts`, `routes/*.ts`, `middleware/*.ts`, `types/*.ts` |
| CLI Tool | `cli.ts`, `commands/*.ts`, `utils/*.ts` |
| Library | `index.ts`, `src/*.ts`, `types.ts` |
| Frontend | `App.tsx`, `components/*.tsx`, `hooks/*.ts` |

---

## Dépannage

### DeepSeek génère un plan flou
→ Ajouter plus de contexte: "Contrainte: TypeScript strict, Style: Clean architecture"

### Qwen2.5-Coder génère du code incomplet
→ Relancer avec: "Continue ce fichier. Code existant: [lignes]"

### Tests échouent
→ Isoler: `pnpm test -- --run -t "test name"`

### Qwen3 génère trop de doc
→ Limiter: "Max 100 lignes, focus installation + usage"

# Dashboard Integration

Le Dev Pipeline envoie des notifications en temps réel au dashboard self-monitoring.

## URL du Dashboard

```
Local:    http://localhost:3001
Tailscale: http://<tailscale-ip>:3001
```

## Visualisation

Le dashboard affiche les 4 agents en temps réel :

```
┌─────────────────────────────────────────────────────────────┐
│                    DEV PIPELINE                              │
├─────────────┬─────────────┬─────────────┬─────────────────────┤
│   LÉONARD   │   GUSTAVE   │    ÉMILE    │    MARGUERITE       │
│   🟢 Actif  │   ⚪ Attente│   ⚪ Attente │    ⚪ Attente        │
│             │             │              │                     │
│ 📖 Analyse: │             │              │                     │
│ "Créer..."  │             │              │                     │
│             │             │              │                     │
│ 🏗️ Arch:    │             │              │                     │
│ - Express   │             │              │                     │
│ - SQLite    │             │              │                     │
│             │             │              │                     │
│ ⏱️ 00:45    │             │              │                     │
└─────────────┴─────────────┴─────────────┴─────────────────────┘
```

Chaque agent a :
- **Statut** : idle, active, waiting, completed, error
- **Logs** : messages en temps réel
- **Progression** : barre de progression
- **Timing** : temps écoulé

## API Endpoints

### Démarrer un pipeline

```bash
POST http://localhost:3001/api/pipeline/start
Content-Type: application/json

{
  "task": "Créer une API REST pour gérer des todos"
}
```

### Ajouter un log

```bash
POST http://localhost:3001/api/pipeline/log
Content-Type: application/json

{
  "agentIndex": 0,
  "type": "info",
  "message": "📖 Analyse du contexte en cours...",
  "details": "Lecture de package.json et README.md"
}
```

Types de log : `info`, `success`, `warning`, `error`, `progress`

### Mettre à jour le statut

```bash
POST http://localhost:3001/api/pipeline/status
Content-Type: application/json

{
  "agentIndex": 0,
  "status": "active",
  "currentTask": "Analyse du contexte",
  "progress": 50
}
```

Statuts : `idle`, `active`, `waiting`, `completed`, `error`

### Passer à l'étape suivante

```bash
POST http://localhost:3001/api/pipeline/next
```

### Terminer le pipeline

```bash
POST http://localhost:3001/api/pipeline/complete
Content-Type: application/json

{
  "summary": {
    "filesCreated": 5,
    "linesOfCode": 450,
    "testsPassed": 12,
    "testsFailed": 0,
    "coverage": 87,
    "documentsGenerated": 3
  }
}
```

### Réinitialiser

```bash
POST http://localhost:3001/api/pipeline/reset
```

### Obtenir l'état actuel

```bash
GET http://localhost:3001/api/pipeline/state
```

## WebSocket Events

Le dashboard se connecte automatiquement au WebSocket et reçoit :

- `pipeline:started` - Pipeline démarré
- `pipeline:update` - Mise à jour (nouveau log, statut)
- `pipeline:step` - Passage à l'étape suivante
- `pipeline:completed` - Pipeline terminé
- `pipeline:error` - Erreur dans le pipeline
- `pipeline:reset` - Pipeline réinitialisé

## Utilisation dans le Skill

Le skill `dev-pipeline` utilise ces endpoints automatiquement pour notifier le dashboard à chaque sous-étape.

Exemple d'intégration dans le skill :

```typescript
// Démarrer le pipeline
await fetch('http://localhost:3001/api/pipeline/start', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ task: 'Créer une API REST' })
})

// Log de Léonard (agentIndex 0)
await fetch('http://localhost:3001/api/pipeline/log', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({
    agentIndex: 0,
    type: 'info',
    message: '📖 Analyse du contexte en cours...'
  })
})

// Passer à Gustave (agentIndex 1)
await fetch('http://localhost:3001/api/pipeline/next')
```

## Avantages

1. **Visibilité totale** : Voir les agents travailler en temps réel
2. **Debug facile** : Logs détaillés par agent
3. **Timing** : Savoir combien de temps chaque étape prend
4. **Résumé final** : Stats complètes à la fin du pipeline
# Guide de Partage - Dev Pipeline

## Pour les copains

### Prérequis

1. **OpenClaw installé** — [docs.openclaw.ai](https://docs.openclaw.ai)
2. **Ollama** — [ollama.ai](https://ollama.ai)
3. **Modèles installés**:
   ```bash
   ollama pull deepseek-r1:8b
   ollama pull qwen2.5-coder:7b
   ollama pull qwen3:8b
   ```

### Installation du skill

**Option A: Copier le dossier**
```bash
cp -r ~/.openclaw/skills/dev-pipeline/ ~/.openclaw/skills/
```

**Option B: Télécharger depuis ClawHub** (si publié)
```bash
clawhub install dev-pipeline
```

### Usage

**AUTOMATIQUE** - Pas de phrases magiques nécessaires.

Le pipeline se déclenche automatiquement pour toute tâche de développement :

```
"Crée une API REST"
"Ajoute l'authentification OAuth2"
"Implémente un système de cache"
```

**Détection automatique**:
- Verbes: créer, ajouter, implémenter, développer, coder
- Sujets: API, feature, système, module, service
- Le mot "pipeline" n'est pas nécessaire

Le skill détecte que c'est du dev et lance automatiquement les 4 étapes.

### Workflow

1. **Léonard** (DeepSeek-R1) analyse et planifie
2. **Gustave** (Qwen2.5-Coder) implémente le code
3. **Émile** (Tests) valide le code
4. **Marguerite** (Qwen3) documente le projet

### Contraintes

- **RAM**: 16 GB minimum (un seul modèle à la fois)
- **Stockage**: ~15 GB pour les 3 modèles
- **Séquentiel**: Pas de parallélisme

### Personnalisation

Éditer `references/prompts.md` pour adapter les prompts à votre style.

### Support

- GitHub: [EdouardF/dev-pipeline](https://github.com/EdouardF/dev-pipeline)
- OpenClaw Discord: [discord.com/invite/clawd](https://discord.com/invite/clawd)

---

## Architecture du Skill

```
dev-pipeline/
├── SKILL.md              # Documentation principale
├── references/
│   ├── prompts.md        # Templates de prompts par étape
│   └── examples.md       # Exemples concrets d'usage
└── SHARE.md              # Ce guide de partage
```

### SKILL.md

- Déclencheurs (phrases qui activent le skill)
- Workflow détaillé
- Commandes Ollama
- Gestion d'erreurs

### references/prompts.md

- Templates par étape (Analyse, Implémentation, Tests, Documentation)
- Prompts de récupération (si modèle répond mal)
- Checklist de qualité

### references/examples.md

- Exemples concrets (API REST, Cache Redis, OAuth2)
- Patterns récurrents par type de projet
- Guide de dépannage

---

## Licence

MIT — Faites ce que vous voulez, partagez, améliorez.

---

## Crédits

Créé par Thierry (assistant IA d'Edouard Forgeau) — 2026-04-10

Inspiré par:
- OpenClaw TaskFlow
- AgentSkills spec
- Architecture multi-agent LLM

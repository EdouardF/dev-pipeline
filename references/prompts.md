# Templates de Prompts par Étape

## Étape 1: Analyse (DeepSeek-R1)

### Prompt Principal

```
Tu es un architecte logiciel senior. Analyse cette tâche et fournis un plan structuré.

Tâche: [DESCRIPTION]

Contexte du projet:
[README ou structure de dossiers]

Fournis:
1. **Compréhension**: Reformule le besoin en 2-3 phrases
2. **Architecture**: 
   - Composants principaux
   - Flux de données
   - Patterns à utiliser
3. **Fichiers**:
   - Liste des fichiers à créer avec leur rôle
   - Ordre de création recommandé
4. **Dépendances**: Packages/libraries nécessaires
5. **Risques**: Edge cases et points d'attention

Format de sortie: JSON structuré
```

### Exemple Concret

```
Tu es un architecte logiciel senior. Analyse cette tâche et fournis un plan structuré.

Tâche: Créer une API REST pour gérer des todos avec authentification JWT

Contexte du projet:
- Node.js + Express + TypeScript
- Base de données: SQLite (fichier)
- Tests: Vitest

Fournis:
1. **Compréhension**: Reformule le besoin en 2-3 phrases
2. **Architecture**: 
   - Composants principaux
   - Flux de données
   - Patterns à utiliser
3. **Fichiers**:
   - Liste des fichiers à créer avec leur rôle
   - Ordre de création recommandé
4. **Dépendances**: Packages/libraries nécessaires
5. **Risques**: Edge cases et points d'attention

Format de sortie: JSON structuré
```

---

## Étape 2: Implémentation (Qwen2.5-Coder)

### Prompt Principal

```
Tu es un développeur senior. Implémente le fichier suivant selon le plan fourni.

Fichier: [FILENAME]
Rôle: [DESCRIPTION DU RÔLE]

Plan global:
[PLAN DE L'ÉTAPE 1]

Code existant dans le projet:
[FICHIERS EXISTANTS PERTINENTS]

Règles de codage:
1. Code clean et lisible
2. TypeScript strict si applicable
3. Gestion d'erreurs robuste
4. Commentaires pour la logique complexe
5. Types exportés pour les interfaces publiques

Fournis uniquement le code, sans explications supplémentaires.
```

### Prompt pour Tests Unitaires

```
Tu es un développeur senior. Écris les tests unitaires pour ce fichier.

Fichier à tester: [FILENAME]
Code du fichier:
[CODE DU FICHER]

Framework de test: [Vitest/Jest/pytest/etc.]

Règles:
1. Coverage minimum 80%
2. Tests happy path + edge cases
3. Mock les dépendances externes
4. Noms de tests descriptifs

Fournis uniquement le code de test.
```

---

## Étape 3: Validation

### Analyse d'Échec de Tests

```
Analyse ces erreurs de test et propose des corrections.

Tests échoués:
[OUTPUT DES TESTS]

Code concerné:
[FICHIERS PERTINENTS]

Propose:
1. Cause racine de chaque erreur
2. Corrections à apporter
3. Fichiers à modifier

Format: JSON avec corrections proposées
```

---

## Étape 4: Documentation (Qwen3)

### Prompt Principal

```
Tu es un technical writer. Génère la documentation pour ce projet.

Projet: [NOM DU PROJET]
Description: [DESCRIPTION]

Fichiers implémentés:
[LISTE DES FICHIERS AVEC BRÈVE DESCRIPTION]

Architecture:
[RÉSUMÉ DE L'ÉTAPE 1]

Résultats des tests:
[RÉSUMÉ DE L'ÉTAPE 3]

Génère:

## 1. README.md
- Titre et description (1-2 phrases)
- Installation rapide (commandes)
- Usage basique (exemples de code)
- Configuration (env vars si applicable)
- Licence (MIT)

## 2. TESTING.md
- Commandes de test
- Coverage attendue
- Comment lancer les tests
- Comment ajouter des tests

## 3. ARCHITECTURE.md
- Structure des dossiers
- Composants principaux
- Flux de données (diagramme texte si besoin)
- Décisions architecturales
- Points d'extension futurs

Format: Markdown propre, headers clairs, exemples de code inline.
```

### Mise à jour MEMORY.md

```
Tu es un assistant qui maintient une mémoire de projet.

Projet: [NOM]
Changements: [DESCRIPTION DES CHANGEMENTS]

Mets à jour ce fichier MEMORY.md en ajoutant une section pour ce projet:

[CONTENU ACTUEL DE MEMORY.md]

Ajoute:
- Nom du projet
- Stack technique
- Structure des fichiers
- Commandes importantes
- Notes de développement

Format: Markdown concis, bullet points.
```

---

## Prompts de Récupération

### Si DeepSeek ne répond pas

```
Simplifie ta réponse. Donne uniquement:
1. Liste des fichiers (format: chemin - rôle)
2. Dépendances (format: package@version)
3. Risques majeurs (max 3)

Pas de JSON, pas d'explications.
```

### Si Qwen2.5-Coder génère du code incomplet

```
Continue le code exactement où tu t'es arrêté. 
Ne répète pas ce qui précède.
Commence par: [DERNIÈRE LIGNE]
```

### Si Qwen3 génère trop de documentation

```
Résume en 50 lignes maximum par fichier.
Focus sur: installation, usage, architecture.
Supprime: historique, roadmap, troubleshooting générique.
```

---

## Checklist de Qualité

### Avant Étape 2

- [ ] Plan clair avec fichiers identifiés
- [ ] Dépendances listées
- [ ] Architecture validée

### Avant Étape 3

- [ ] Tous les fichiers créés
- [ ] Code compile sans erreur
- [ ] Imports corrects

### Avant Étape 4

- [ ] Tests passent
- [ ] Pas de console.log oublié
- [ ] Types corrects (si TypeScript)

### Après Pipeline

- [ ] README.md existe et est à jour
- [ ] TESTING.md existe
- [ ] ARCHITECTURE.md existe
- [ ] MEMORY.md mis à jour (si applicable)
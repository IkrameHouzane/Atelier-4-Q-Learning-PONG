# Atelier 4 : Q-Learning / PONG
## Description

Implémentation de l'algorithme **Q-Learning** pour contrôler un agent intelligent dans le jeu **PONG**. L'agent apprend à jouer en interagissant avec l'environnement et en maximisant les récompenses cumulées.

## Modes de jeu

1. **Agent RL vs Agent AI** : L'agent Q-Learning joue contre une IA simple qui suit la balle
2. **Agent RL vs Human** : L'agent joue contre un joueur humain (contrôles clavier)
3. **Agent RL vs Agent RL** : Deux agents Q-Learning s'affrontent

## Structure du projet

```
Atelier4_QLearning_Pong/
├── agent.py          # Classe Qlearning avec algorithme Q-Learning
├── game.py           # Classe Game - environnement Pong avec pygame
├── main.py           # Script principal d'entraînement et d'évaluation
├── models/           # Modèles Q-tables sauvegardés
├── figures/          # Graphiques des récompenses
└── README.md         # Ce fichier
```

## Installation

```bash
# Dépendances requises
pip install pygame numpy matplotlib
```

## Utilisation

```bash
# Lancer le menu principal
python main.py
```

### Options du menu :
- **1** : Entraîner RL vs AI
- **2** : Jouer RL vs Human (vous contre l'agent)
- **3** : Entraîner RL vs RL
- **4** : Démonstration d'un agent entraîné
- **5** : Exécuter tous les modes

## Algorithme Q-Learning

### Formule de mise à jour
```
Q(s, a) ← Q(s, a) + α[r + γ·max(Q(s', a')) - Q(s, a)]
```

### Paramètres
- **α (alpha)** : Taux d'apprentissage (0.5)
- **γ (gamma)** : Facteur de discount (0.95)
- **ε (epsilon)** : Taux d'exploration (0.3 → décroissance)

### Système de récompenses
| Événement | Récompense |
|-----------|------------|
| Agent IA gagne | -1 |
| Player gagne | +1 |
| Player touche la balle | +0.1 |
| Autres cas | 0 |

### Représentation de l'état
L'état est discrétisé pour réduire l'espace d'états :
- Position de la balle (x, y) en zones
- Direction de la vélocité de la balle
- Position de la raquette du joueur
- Position relative balle/raquette

### Sélection d'action (ε-greedy)
- Avec probabilité ε : action aléatoire (exploration)
- Sinon : action avec Q-value maximale (exploitation)

## Résultats

Les graphiques générés incluent :
- **Récompense cumulative** vs épisodes
- **Moyenne mobile** des récompenses
- **Taux de victoire** au fil du temps
- **Comparaison** entre les modes

## Contrôles (Mode Human)

- **↑** : Monter la raquette
- **↓** : Descendre la raquette

## Fichiers

### agent.py
Implémente la classe `Qlearning` avec :
- `get_action(state)` : Sélection ε-greedy
- `update(s, s_, a, a_, r)` : Mise à jour Q-Learning
- `save()/load()` : Persistance de la Q-table

### game.py
Implémente la classe `Game` avec :
- `getStateKey()` : Représentation de l'état
- `step(action)` : Exécution d'une action
- `reset()` : Réinitialisation de l'épisode
- Support des 3 modes de jeu

### main.py
- `plot_agent_reward()` : Visualisation des récompenses
- `GameLearning` : Orchestration de l'entraînement
- Modes d'entraînement et de démonstration


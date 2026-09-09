# AGI Workbench commun — résumé

## 1. But

Le **workbench** est une petite infrastructure commune pour tester des approches très différentes de l’AGI sans réécrire tout le protocole expérimental à chaque fois.

L’idée centrale :

> **même problème + même protocole + même évaluateur**, mais chaque système reste libre d’utiliser sa représentation et son algorithme propres.

Le workbench ne cherche donc pas à imposer le même modèle de données interne à un LLM, Dreamer, Soar, un système symbolique, etc.

---

## 2. Ce qui doit être commun

Pour comparer deux approches proprement, on fixe autant que possible :

- les **mêmes tâches / instances** ;
- les **mêmes splits** (`train`, `dev`, `test`, holdout) ;
- les **mêmes observations accessibles** ;
- les **mêmes limites de ressources** : nombre d’actions, temps, tokens, calcul, mémoire, etc. ;
- les **mêmes métriques** ;
- le **même Runner** et le **même Evaluator**.

**Important :** « mêmes données » ne signifie pas que chaque système doit recevoir exactement le même tenseur ou le même format interne. Ils reçoivent la même information de départ, puis peuvent l’encoder différemment.

---

## 3. Architecture minimale

```text
Benchmark / Task
      ↓
Observation
      ↓
System / ModelAdapter
      ↓
Action
      ↓
Runner
      ↓
Transition / Episode / Trajectory
      ↓
Evaluator
      ↓
Metrics + logs + résultats
```

### Les objets essentiels

- **Task** : le problème à résoudre.
- **Observation** : l’information disponible à un instant donné.
- **Action** : ce que le système décide de faire.
- **Transition** : `(observation, action, observation suivante, résultat)`.
- **Episode** : une exécution complète d’une tâche interactive.
- **Trajectory** : la suite des transitions d’un épisode.
- **Budget** : les ressources maximales autorisées.
- **Metric** : une mesure de performance.

Pour une tâche non interactive, une `Task` peut simplement contenir une entrée et une sortie attendue ; il n’est pas nécessaire de simuler artificiellement des épisodes.

---

## 4. Interface commune des systèmes

Le contrat doit rester très petit :

```python
class System:
    def reset(self, task): ...
    def act(self, observation): ...
    def observe(self, transition): ...
    def end_episode(self): ...
```

Chaque approche est branchée derrière un **adapter** :

```text
systems/
    llm/
    symbolic/
    world_model/
    cognitive/
    causal/
    evolutionary/
    neuroai/
```

Un adapter traduit simplement l’interface commune vers l’API native du modèle ou du framework étudié.

---

## 5. Deux types de benchmarks

### Offline

Exemples : raisonnement, ARC statique, synthèse de programmes, classification causale.

```text
input → système → réponse → score
```

### Interactifs

Exemples : ARC-AGI-3, gridworlds, agents, robotique simulée, RL.

```text
observation → action → environnement → nouvelle observation → ...
```

Le workbench doit supporter les deux sans forcer l’un à ressembler à l’autre.

---

## 6. Structure du dépôt

```text
agi-workbench/
├── core/
│   ├── types.py
│   ├── task.py
│   ├── system.py
│   ├── runner.py
│   ├── evaluator.py
│   └── budget.py
├── benchmarks/
│   ├── arc/
│   ├── gridworld/
│   ├── reasoning/
│   ├── causal/
│   └── ...
├── systems/
│   ├── llm/
│   ├── symbolic/
│   ├── world_model/
│   └── ...
├── experiments/
└── results/
```

---

## 7. Ce que le workbench ne doit pas devenir

Il ne faut pas construire un nouveau framework gigantesque.

Le cœur doit rester **très mince** : idéalement de l’ordre de **1 000 à 2 000 lignes**. Les frameworks spécialisés restent utilisés derrière les adapters : PyTorch, Gymnasium, Hugging Face, Soar, Pyro, etc.

Le workbench sert uniquement à standardiser :

> **les tâches, l’exécution, les budgets, les traces et l’évaluation.**

---

## 8. Principe directeur

Quand on ajoute une nouvelle voie de recherche, on ne modifie normalement pas le Runner ni l’Evaluator.

On ajoute seulement :

1. un **benchmark** si la tâche est nouvelle ;
2. un **SystemAdapter** pour l’approche étudiée ;
3. une configuration d’expérience.

Ainsi, les différentes voies vers l’AGI peuvent être étudiées dans un même laboratoire expérimental, sans prétendre qu’elles fonctionnent toutes de la même manière.

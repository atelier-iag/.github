# Voies vers l’AGI — plan de pratique

Objectif : pour chaque voie, partir d’un projet ou modèle existant, reproduire une baseline, puis réimplémenter les mécanismes centraux et une amélioration moderne.

| # | Voie | Point de départ conseillé | Ce que tu dois t’approprier |
|---|---|---|---|
| **1** | **Modèles de fondation / scaling** | **OLMo 3**, via une version miniature | Tokenizer, données, préentraînement, Transformer decoder, RoPE/GQA, mixed precision, scaling laws, continued pretraining, SFT et post-entraînement. |
| **2** | **Raisonnement délibératif** | **Open-R1** + recette **DeepSeek-R1/R1-Zero** | RLVR/GRPO, récompenses vérifiables, self-consistency, vérificateur/reranker, test-time compute adaptatif. |
| **3** | **Agents et outils** | Réimplémenter **ReAct**, puis étudier **OpenHands** et **BrowserGym** | Boucle observer–raisonner–agir, outils, état persistant, mémoire, planification, sandbox, reprise après erreur, évaluation par trajectoires. |
| **4** | **Modèles du monde / model-based RL** | **DreamerV3**, puis **TD-MPC2** | RSSM, dynamique latente, trajectoires imaginées, actor-critic latent, MPC/CEM, incertitude. |
| **5** | **Robotique et intelligence incarnée** | **LeRobot** + **SmolVLA** ou **OpenVLA-OFT** | Démonstrations, behavior cloning, action chunking, diffusion policy, VLA, contrôle temps réel, simulation → robot. |
| **6** | **Symbolique et neuro-symbolique** | **DreamCoder**, **Lean/Z3**, puis **AlphaGeometry2** | DSL, recherche symbolique, exécution, vérification formelle, propositions neuronales, abstraction et génération synthétique. |
| **7** | **Causal et probabiliste** | **Pyro/NumPyro** + **DoWhy** | Programmation probabiliste, VI/MCMC, modèles causaux structurels, interventions `do`, contrefactuels, découverte causale. |
| **8** | **Apprentissage continu, méta et open-ended** | **Avalanche → MAML → POET/OMNI-EPIC** | Replay, EWC/LwF, adapters, oubli catastrophique, méta-apprentissage, curricula automatiques, nouveauté et transfert. |
| **9** | **Architectures cognitives** | **Soar**, puis **ACT-R**, **NARS** ou **Hyperon** | Règles de production, mémoires, buts, chunking, sélection d’opérateurs, métacognition, intégration perception–décision–action. |
| **10** | **Modularité, MoE et Society of Mind** | **OLMoE**, en étudiant aussi **DeepSeek-V3** | Experts sparse, routage top-k, équilibrage, spécialisation, expert parallelism, puis routage entre agents spécialisés. |
| **11** | **NeuroAI et neuromorphique** | **Monty**, **pymdp**, **snnTorch/Lava** | Représentations sensorimotrices, active inference, expected free energy, neurones LIF, STDP, surrogate gradients. |
| **12** | **Évolution et auto-amélioration** | **EvoTorch → OpenEvolve → Darwin Gödel Machines** | CMA-ES/MAP-Elites, novelty search, archives, populations, mutations proposées par LLM, évaluateurs automatiques, auto-modification validée en sandbox. |

## Critère de maîtrise commun

Pour chaque voie : **reproduire une baseline → réimplémenter l’algorithme central → ajouter une amélioration moderne → faire une ablation → tester sur un holdout**.

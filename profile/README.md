# Plan général — appropriation des [voies vers l’AGI](./AGI_voies_pratique.md)

## Objectif

Construire une compréhension **pratique et comparable** des [principales approches vers l’AGI](./AGI_voies_pratique.md), puis utiliser cette base pour identifier des combinaisons et des questions de recherche intéressantes.

Les laboratoires suivent le [contrat commun](https://github.com/atelier-iag/.github/blob/main/LAB_CONTRACT.md), qui définit leur structure et leur progression.

## Plan général

1. **Construire le [workbench commun](./AGI_Workbench_Commun.md)**
   - mêmes tâches, splits, budgets, métriques et format de résultats ;
   - chaque système s’y branche via un adaptateur simple.

2. **Parcourir les [laboratoires / voies](./AGI_voies_pratique.md) un par un**
   - partir d’un projet / modèle de référence ;
   - reproduire une baseline ;
   - réimplémenter le mécanisme central ;
   - ajouter au moins une technique moderne importante ;
   - tester avec le protocole commun ;
   - faire une ou deux ablations et documenter les échecs.

3. **Comparer les laboratoires**
   - repérer leurs forces, limites et régimes d’échec ;
   - identifier les mécanismes réellement complémentaires ;
   - éviter les comparaisons faussées par des budgets ou données différents.

4. **Passer à la recherche**
   - combiner les mécanismes qui semblent complémentaires ;
   - formuler des hypothèses falsifiables ;
   - construire des expériences et ablations capables de les départager ;
   - conserver uniquement les idées qui améliorent réellement la généralisation ou l’efficacité.

## Quand considère-t-on un laboratoire comme « maîtrisé » ?

Un laboratoire est maîtrisé lorsque je peux :

- **expliquer** son idée centrale et ses hypothèses ;
- **faire fonctionner** une implémentation de référence ;
- **réimplémenter** le mécanisme principal sans dépendre de son code d’origine ;
- **reproduire** une baseline raisonnable ;
- **implémenter une amélioration moderne** et mesurer son effet ;
- **faire des ablations** pour comprendre ce qui compte réellement ;
- **diagnostiquer les échecs** plutôt que seulement regarder un score ;
- **tester sur des données / tâches tenues à l’écart** ;
- conserver une **implémentation minimale + une note courte** servant de référence personnelle.

> Le but n’est pas de reproduire les budgets des grands laboratoires, mais de maîtriser les mécanismes suffisamment bien pour les comparer, les modifier et éventuellement les combiner.

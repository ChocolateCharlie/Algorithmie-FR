---
title: Complexité algorithmique
permalink: /generalites/complexite-algorithmique
published: false
---

# Complexité algorithmique

_L'objectif du présent article est de fournir à des débutants disposant d'un bagage en mathématiques hétérogène les bases en analyse de la complexité d'un algorithme.
Il ne s'agira ici nullement de traiter le sujet - particulièrement vaste - en profondeur, ni même d'amener le lecteur à réaliser par lui-même de telles analyses (même si, bien sûr, une bonne compréhension et un peu de pratique devraient suffire pour procéder à des analyses élémentaires).
Ainsi, cet article se bornera simplement à donner les quelques éléments nécessaires à la compréhension des analyses de complexité des divers algorithmes présentés sur ce blog afin de les rendre les plus abordables possible._

_Il est à noter que **la complexité algorithmique est un sujet difficile.**
Il est donc parfaitement normal de revenir de temps à autre à cet article lors de votre lecture sur ce blog.
Et qui sait, peut-être qu'un jour vous aurez le courage de vous y mettre "une bonne fois pour toute"_ :wink:

_Notez que, malgré ma volonté de m'adresser à des débutants, un certain formalisme (et raisonnement) mathématique sera préservé.
En effet, on trouve nombre d'introductions à l'analyse de la complexité algorithmique sur le web qui, sous prétexte de simplifier ce sujet intrinsèquement complexe, se bornent à énumérer tel un catalogue les analyses les plus fréquemment rencontrées.
Or, ce genre d'approche n'aident pas davantage à **comprendre** comment réaliser une telle analyse.
Ce sont simplement les résultats d'une démarche exposés tels quels, sans expliquer pour autant en quoi consiste ladite démarche.
**Vous ne progresserez pas en algorithmie en apprenant par coeur des résultats.**
C'est pourquoi je m'efforcerai ici d'expliquer comment fonctionne une telle analyse quitte à n'atteindre que des résultats "simples".
Les autres résultats seront exposés à chaque présentation d'un nouvel algorithme sur ce blog, ce qui vous permettra de progresser par la pratique.
De plus, pour ceux qui seraient davantage intéressés par la théorie, je vous fournirai également quelques références dans la section "liens externes"._

_**Remarque :**
Si un peu d'intuition devrait suffire au plus débrouillards, je vous recommande tout de même de jeter un coup d'oeil aux concepts mathématiques suivants avant d'entreprendre votre lecture : limite d'une fonction, polynôme, exponentielle, logarithme.
Il n'y aura pas (ou très peu) de calculs afin de ne pas entraver la compréhension du plus grand nombre._

_Bonne lecture !_ :bar_chart: :chart_with_upwards_trend:

---

## Pourquoi analyser un algorithme ?

L'une des différences fondamentales entre un programmeur réellement compétent et un novice réside dans la maîtrise des fondamentaux en algorithmie.
Or l'analyse de la complexité, c'est-à-dire la prédiction des ressources requises par un algorithme donné pour s'exécuter convenablement, en fait partie.

> :warning: **mieux définir la complexité pour la suite** :warning:

En effet, en informatique, le temps (que met un programme à s'exécuter) et la mémoire (dont dispose un ordinateur) sont des ressources limitées.
Par conséquent, tout bon programmeur se doit d'être attentif quant à l'usage de ces ressources, notamment en utilisant des algorithmes efficaces en termes de temps et de mémoire (aussi appelée "espace", comme dans l'expression "espace de stockage").

Si vous connaissez  [la loi de Moore](https://fr.wikipedia.org/wiki/Loi_de_Moore), vous pourriez objecter que les ordinateurs évoluent suffisamment rapidement pour que de telles considérations soient vaines.
Néanmoins, que faites-vous si la complexité de votre algorithme croit plus vite que cette loi ?
Vous ne pourrez pas attendre quelques années que les ordinateurs deviennent plus puissant, il vous faut un nouvel algorithme.
Vous allez donc chercher à concevoir un nouvel algorithme **plus efficace**, c'est-à-dire qui s'exécute plus rapidement.
Or, si vous n'êtes pas en mesure d'anticiper le temps d'exécution d'un algorithme, vous n'allez pas pouvoir comparer les algorithmes entre eux, ni prédire lequel s'exécute le plus rapidement (ou avec un délai raisonnable).
Il vous faut donc un moyen pour pouvoir **comparer les algorithmes entre eux**.
Et là, vous n'avez pas le choix : pour savoir si un algorithme est efficace, le seul moyen est de l'**analyser**.

Cette situation est malheureusement loin de faire exception, et il n'est pas rare que l'algorithme le plus simple ait une complexité très mauvaise, c'est-à-dire qu'il prenne beaucoup de temps à s'exécuter.

_**Remarque :**
Dans le cadre des compétitions de programmation, vous aurez probablement déjà remarqué qu'un certain temps et une certaine quantité de mémoire vous sont alloués et qu'il n'est bien sûr par permis d'en utiliser davantage._

## Comment analyser un algorithme ?

### Un moyen simple pour exprimer la durée d'exécution d'un algorithme

Analyser un algorithme, même simple, n'est pas évident.
En effet, les algorithmes peuvent se comporter de manière différente selon l'entrée.
Par conséquent, il nous faut résumer l'ensemble de ces comportements possibles en des **formules simples et faciles à comprendre**.
Pour cela, on utilise des **fonctions** (plus précisément des [fonctions réelles d'une variable réelle](https://fr.wikipedia.org/wiki/Fonction_r%C3%A9elle_d%27une_variable_r%C3%A9elle)).
Les fonctions sont un outils mathématique qui prennent une entrée et, en appliquant un calcul (défini par la fonction), donnent une sortie.

_**Remarque :**
Oui, les fonctions dont je vous parle en mathématiques sont analogues aux fonctions (ou méthodes) dont on parle en informatique !_

Ici, nos fonctions vont avoir pour **entrée** _n_, la taille de l'entrée de notre algorithme.
> Par exemple, si on écrit un algorithme qui cherche un mot parmi une liste de mots, _n_ est la taille de cette liste.
> Ou encore, dans algorithme qui calcule les termes d'une suite, _n_ est n-ième terme qu'on veut calculer.

Et en **sortie**, les fonctions nous donnent le temps que met l'algorithme à s'exécuter donc... exactement ce que l'on cherche ! :smile: :sparkles:

_**Remarque :**
Vous aurez compris qu'on choisit la taille de l'entrée comme_ n _car plus l'entrée est grande, plus l'algorithme prendra de temps à s'exécuter (logique).
Par conséquent, le résultat que nous cherchons (la durée d'exécution de l'algorithme) dépend de la taille de l'entrée_ n _._

Mais quel est ce calcul magique qui vous permettra de déduire le temps que prend votre algorithme à s'exécuter ?
C'est là que les choses se compliquent... car ce calcul, c'est à vous de le faire.
Mais, ne vous inquiétez pas, nous allons voir tout cela ensemble, pas à pas :wink:

### Trouver la fonction dans l'algorithme

Compter les étapes élémentaires.

### Qu'est-ce qu'une étape élémentaire ?

Les étapes élémentaires sont en réalité déjà une simplification.
En effet, elles sont exprimées par rapport à du pseudo-code.
Le temps que prend chaque étape dépend principalement du processeur utilisé (donc de la machine), et même de "détails" tels que la façon dont est géré la mémoire cache.
Par conséquent, prendre en compte toutes ces spécificités liées à l'architecture (de l'ordinateur utilisé) serait un cauchemar.
De plus, le résultat ainsi obtenu ne pourrait pas être généralisé d'une machine à une autre...
C'est donc pour cela qu'on exprime le temps d'exécution par rapport à des "étapes élémentaires", lesquelles peuvent en réalité prendre un temps plus ou moins variable, mais toujours court.
Il s'agit donc d'une manière de réaliser une **bonne approximation**.

## Comparaison asymptotique pour les non-matheux

_Cette notion sera abordée de manière assez peu "mathématique" afin de la rendre abordable au plus grand nombre.
Mes excuses à ceux qui pourraient s'offusquer de l'évident manque de rigueur des lignes à suivre._

### Comment simplifier une fonction ?

Voici quelques règles que vous proposent Dasgupta & Papadimitriou pour simplifier les fonctions en écartant les termes les moins importants :
  - Ne pas tenir compte des constantes multiplicatives. _Exemple : 7n^3 devient n^3_
  - n^a est plus important que n^b si a > b. _Exemple : n^2 + n devient n^2_
  - Les exponentielles sont plus importantes que n'importe quel polynôme. _Exemple : 2^n + n^7 devient 2^n_
  - De manière analogue, les polynômes sont plus importants que n'importe quel logarithme. _Exemple : n^2 + n log(n) devient n^2_


### Pourquoi choisir le pire des cas ?

## Conclusion

Face à un algorithme, Dasgupta et Papadimitriou vous conseillent de toujours vous poser trois questions :
  - Est-il correct ? c'est-à-dire : a-t-il une fin ? et : est-ce que la sortie est toujours la bonne réponse ?
  - Combien de temps prend-il pour s'exécuter, exprimé en fonction de la taille de l'entrée ? (idem pour la mémoire)
  - Est-il possible de mieux faire ? c'est-à-dire : est-il possible de concevoir un algorithme plus rapide ou qui consomme moins de mémoire ?

---

### Liens externes
:fr:
  - Le chapitre sur la [notion de complexité](https://openclassrooms.com/fr/courses/1467201-algorithmique-pour-lapprenti-programmeur/1467358-la-notion-de-complexite) du cours d'[algorithmique pour l'apprenti programmeur](https://openclassrooms.com/fr/courses/1467201-algorithmique-pour-lapprenti-programmeur) sur OpenClassrooms (tous niveaux) :warning: faire la MAJ car le cours sera bientôt archivé :warning:
  - L'article sur la [complexité d'un algorithme](https://info.blaisepascal.fr/nsi-complexite-dun-algorithme) sur le site du lycée Blaise Pascal de Clermont-Ferrand (niveau lycée)
  - L'article sur la [complexité algorithmique](http://www.monlyceenumerique.fr/nsi_premiere/algo_a/a2_complexite.php) sur le site Mon Lycée Numérique (niveau lycée)
  - Le cours de [structures de données et algorithmes fondamentaux](http://igm.univ-mlv.fr/~alabarre/teaching/struct/poly-m1103.pdf) d'Anthony Labarre à l'IUT de Marne-la-Vallée (niveau 1ère année de DUT Informatique)
  - Le cours sur la [notion de complexité algorithmique](http://www.monlyceenumerique.fr/nsi_premiere/algo_a/a2_complexite.php) de Jean-Pierre Becirspahic au lycée Louis-Le-Grand (niveau MPSI)
  - Le cours de [complexité algorithmique](https://bouchflo.gricad-pages.univ-grenoble-alpes.fr/L2-algo/download/Documents/03-Complexite.pdf) de Florent Bouchez Tichadou à l'Université Grenoble Alpes (niveau L2)
  - Le livre [Complexité algorithmique](https://www.irif.fr/~sperifel//complexite.pdf) de Sylvain Perifel (niveau très avancé...)

:uk:
  - [StackOverflow](https://stackoverflow.com/questions/487258/what-is-a-plain-english-explanation-of-big-o-notation)
  - [Big-O Cheat Sheet](https://www.bigocheatsheet.com/)

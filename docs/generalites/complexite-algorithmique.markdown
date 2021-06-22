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

_Vous avez sans doute déjà remarqué que la plupart des concepts en informatique sont présentés selon une approche similaire d'un manuel à l'autre.
Pour ce qui est de la complexité algorithmique, les chapitres dédiés à ce sujet diffèrent grandement selon les ouvrages, tantôt privilégiant un formalisme mathématique particulièrement rebutant pour le novice, tantôt se lançant d'emblée dans une mise en pratique noyant l'essence de la démarche dans des considérations liées au problème spécifiquement choisi en guise d'illustration.
Je m'efforcerai donc ici de préserver un certain équilibre entre ces deux aspects, afin de rendre le plus clair possible mon propos.
Ainsi, en dépit de ma volonté de m'adresser à des débutants, un certain formalisme (et raisonnement) mathématique sera préservé.
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

_Bonne lecture !_

---

## Introduction : pourquoi analyser un algorithme ?

L'une des différences fondamentales entre un programmeur réellement compétent et un novice réside dans la maîtrise des fondamentaux en algorithmie.
Or l'analyse de la complexité, c'est-à-dire la prédiction des ressources requises par un algorithme donné pour s'exécuter convenablement, en fait partie.
En effet, en informatique, le temps (que met un programme à s'exécuter) et la mémoire (dont dispose un ordinateur) sont des ressources limitées.
Par conséquent, tout bon programmeur se doit d'être attentif quant à l'usage de ces ressources, en utilisant des algorithmes efficaces en termes de temps et de mémoire (aussi appelée "espace", comme un un espace de stockage).

Si vous connaissez  [la loi de Moore](https://fr.wikipedia.org/wiki/Loi_de_Moore), vous pourriez objecter que les ordinateurs évoluent suffisamment rapidement pour que de telles considérations soient vaines.
Néanmoins, que faites-vous si la complexité de votre algorithme croit plus vite que cette loi ?
Vous ne pourrez pas attendre quelques années que les ordinateurs deviennent plus puissant, il vous faut un nouvel algorithme.
Et, pour ce faire, il vous faut :
  1) déterminer le temps d'ex

_**Remarque :** dans le cadre des compétitions de programmation, vous aurez probablement déjà remarqué qu'un certain temps et une certaine quantité de mémoire vous sont alloués._

Analyser un algorithme, même simple, n'est pas évident.
En effet, les algorithmes peuvent se comporter de manière différente selon l'entrée.
Par conséquent, il nous faut résumer l'ensemble de ces comportements possibles en des **formules simples et faciles à comprendre**.




### Liens externes
En cours

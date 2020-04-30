---
title: "Retours sur le Code Retreat 2016"
date: 2016-11-02
tags:
- GDCR
- TDD
description: "Retour sur ma toute première participation au Global Day of Code Retreat"
---
![img](/img/GDCR-2016/feature-coderetreat.png)

Le **Global Day of Code Retreat** est un événement mondial où des développeurs se réunissent pour le plaisir de pratiquer l'artisanat logiciel (**Software Craftmanship**) autour d'un sujet commun - le jeu de la vie - à implémenter par la technique du **TDD** (Test Driven Development), avec quelques contraintes imposées par les facilitateurs (qui portent plutôt mal leur nom du coup).

## TL,DR

  - 115 villes participantes ;
  - 14 développeurs passionnés à Toulouse ;
  - 2 facilitateurs ;
  - 1 samedi complet à coder en TDD ;
  - 6 sessions de 45 min. et 15 min. de retrospective ;
  - 1 repas ;
  - Pleins de choses découvertes.


## Le contexte

Dans le cadre de mon travail chez [**VISEO**](www.viseo.com), je recherche à sponsoriser des événements dédiés aux développeurs. En 2011, un collègue avait fait héberger un **Global Day of Code Retreat** dans mon ancienne boîte et je me suis dit que, cette année, ce serait sympa de faire sponsoriser cet événement par **VISEO**.  
  
Et j'en ai profité pour y participer cette fois-ci.


## Le principe

L'événement consiste à coder loin des contraintes que l'on peut rencontrer en milieu professionnel (stress, tenue des objectifs, produire vite...) pour, non pas produire à tout prix quelque chose qui marche, mais pour faire du **bon code**.  
  
La journée est découpée en sessions de 45 minutes suivies d'une retrospective de 15 minutes. À la fin de chaque session tout le monde supprime son code !!!  
  
Hé oui, c'est dur mais c'est comme ça. Il y a plusieurs raison à cela : d'abord, il ne faut pas se mentir, on n'y reviendra pas plus tard. Ensuite, le but de la journée n'est pas de produire mais apprendre comment faire du beau code et, ce savoir, c'est vous qui le portez.  
  
De plus, avec le recul, on produit tellement peu de code, qui ne marche pas en plus, que ça ne vaut vraiment pas le coup de le conserver.  
  
Et je ne regrette rien, on n'y pense même pas.  
  
À chaque session, change de partenaire, le choix du langage est libre (on en a vu qui ont tenté l'exercice avec des shaders !), ainsi que le choix de l'IDE ou encore de la librairie de test.  
  
À chaque fois, on recommence donc à zéro mais les facilitateurs donnent une contrainte à respecter pour pimenter quelque peu l'exercice.  
  
Et on tente inlassablement d'implémenter le jeu de la vie en pair-programming, avec la technique du TDD.

## Le jeu de la vie

Le jeu de la vie ou **Conway's game of life** (dont on peut voir une [implémentation en Drools ici](http://richard-fagot.github.io/returnfromdeath//le-jeu-de-la-vie-en-drools/)) est un automate cellulaire qui répond à un ensemble de règles, ici 4 (mais il en existe une version avec 2 règles uniquement) :

  - Une cellule vivante qui a moins de 2 voisines meurt par sous-population ;
  - Une cellule vivante qui a exactement plus de 3 voisines meurt par sur-population ;
  - Une cellule vivante qui a 2 ou 3 voisines reste vivante ;
  - Une cellule morte qui a exactement 3 voisines devient vivante.

L'objectif de chaque session est d'implémenter ces règles de la meilleure façon possible avec la contrainte imposée.

## Organisation de la journée

En arrivant sur le lieu de l'événement (un samedi matin à 9h il faut le vouloir !!), un petit déjeuner était offert et on pouvait commencer à faire connaissance en attendant le reste des participants.  
  
Sur un des murs était projeté le flux de plusieurs webcams installées dans divers sites dans le monde ce qui permettait de voir les autres groupes travailler, en en profitant pour se faire des petits coucous au passage :D.  
  
![Webcams Wall](/img/GDCR-2016/webcam.jpg)  
  
C'est plutôt sympa de pouvoir saluer un groupe de personnes venues faire la même chose que vous et se trouvant à des milliers de kilomètres, bonne ambiance !  
  
Cette année, 6 villes Françaises, dont Toulouse, ont participé à l'événement (sur un total de 115 villes participantes).  
  
Après un tour de table pour que chacun se présente, les facilitateurs ont exposé le programme de la journée et les règles du jeu de la vie.  
  
Puis, chacun s'est trouvé un binôme pour commencer la première session (comme on était impair, il y avait un groupe de trois).

## Session 1 : Échauffement

Cette première session est une session de familiarisation avec les règles du jeu de la vie. Normalement, à cette étape, on ne commence pas en TDD (on en n'a pas encore parlé), mais j'étais en trinôme avec un partenaire qui participe aux **Code Retreat** depuis longtemps et pour lui c'était naturel de commencer comme ça.  
  
Il souhaitait en profiter pour tester en **javascript**, moment découverte. On n'a pas vraiment fait le jeu de la vie mais j'ai découvert [**yarn**](https://github.com/yarnpkg/yarn) (un **npm** en mieux il parait) et [**karma**](https://karma-runner.github.io/1.0/index.html) (un test-runner plutôt cool).

## Session 2 : TDD et Ping Pong

À la suite de la restrospective de la session précedente, les facilitateurs nous on expliqué le principe du TDD et nous ont demandé de l'appliquer avec la contrainte de le réaliser en **ping-pong pair programming**.  
  
Le cycle du TDD est composé de trois phases :

  1. Écrire un TU qui échoue ;
  2. Écrire le code minimal qui passe le TU en succés ;
  3. Refactoriser.


Avec le mode **ping-pong pair programming** le premier binôme écrit un test puis passe le clavier au second binôme qui fait passer le test, refactorise et écrit un nouveau test puis rend le clavier au premier binôme qui fait passer le test, refactorise et écrit un nouveau test puis rend le clavier au second binôme, ainsi de suite.  
  
C'était dynamisant, les deux binômes sont physiquement actifs, le travail est tourné sous la forme d'un jeu sérieux en quelque sorte.  
  
Je me suis senti motivé et alerte, les deux binômes continuent de réfléchir ensemble sans qu'il y en ait un qui finisse pas devenir simple spectateur.

## Apparté : Les 4 règles pour un design simple

Dans l'esprit des TDD, il faut toujours essayer de respecter les 4 règles pour un design simple, edictées par [**Ken Beck**](https://fr.wikipedia.org/wiki/Kent_Beck) (inventeur de l'**eXtreme Programming** et du **TDD**) :

   - Les tests doivent passer ;
   - L'intention du développeur doit être claire pour un tiers ;
   - Pas de duplication ;
   - Faire le minimum nécessaire.

Ce n'est pas l'objet de cet article que d'expliquer ces règles, aussi je vous invite à consulter [celui-ci](http://martinfowler.com/bliki/BeckDesignRules.html) pour vous en faire une idée.

## Session 3 : Pas de types primitif

![Pas de types primitif](/img/GDCR-2016/DSC_4115.jpg)  
  
Interdiction formelle d'utiliser des types primitifs dans les arguments des méthodes sous peine de sanctions terribles (genre coder en cobol).  
  
Le principe est d'encapsuler les types primitifs pour gagner en abstraction et, chose que j'ai découverte à cette occasion, pour gagner en **flexibilité**.  
  
Par exemple (un peu simpliste), une cellule est localisée dans le plan grâce à ses coordonnées `(x,y)`, et on code ça :

{{< highlight javascript >}}
  nextState(cell, x, y);
{{< / highlight >}}

Si demain on nous dit d'utiliser un espace en 3 dimensions il faudra passer partout dans le code pour ajouter la variable *z* :

{{< highlight javascript >}}
  nextState(cell, x, y, z);
{{< / highlight >}}

  En encapsulant les types primitifs dans une classe `Position` il suffit de modifier uniquement cette classe pour prendre en compte l'évolution :

{{< highlight javascript >}}
  class Position {
    int x, y, z;
  }

  Position p;
  ...
  nextState(cell, p);
{{< / highlight >}}

Cette session oblige à penser le code différemment en passant à un niveau d'abstraction supérieur en s'appuyant sur le métier qu'on est en train d'implémenter.  
  
Par exemple, avec mon binôme on lisait à haute voix notre test :

> *"Si il y a moins de 3 voisins alors elle est morte."*

Et le facilitateur de nous faire remarquer :

> *"C'est bizarre, vous dites 'morte' et moi je lis 'false'. Il y a peut-être quelque chose à faire là."*

Oui, c'est vrai qu'un `enum (DEAD, ALIVE)` rendrait les choses plus parlantes.

## Pause déjeuner

La pause déjeuner fait partie intégrante de l'événement. Le repas doit être bon (pas de pizza ! ) et on en profite pour échanger sur les sessions qui viennent de passer.  
  
![Pause déjeuner](/img/GDCR-2016/repas.jpg)  
  
Les conversations dérivent rapidement sur les avantages des bonnes pratiques et les difficultés à les faire appliquer en milieu professionnel.  
  
C'est quelque chose que je connais bien en tant qu'ancien développeur professionnel mais que j'avais finalement laissé tombé. Et ça me fait réfléchir.  
  
Aujourd'hui, j'occupe un poste qui me permet de faire changer les choses, et  y étant sensible, je vais en profiter pour les faire appliquer en accord avec les équipes et voir ce qu'il se passe.

## Session 5 : Baby Steps

![Baby Steps](/img/GDCR-2016/DSC_4117.jpg)  
  
Pour nous réveiller après le copieux repas, les facilitateurs nous ont donné comme contrainte de travailler en **Baby Steps**.  
  
Ça a l'air sympa comme ça des baby steps - des pas de bébé, comme c'est meugnon ! - mais en fait, c'est mortel.  
  
Le principe : on a deux minutes pour faire un cylce TDD complet (hors refactoring) plus un commit. Si les tests ne passent pas ou qu'on n'a pas eu le temps de commiter on a le droit à un `git reset --hard` et il faut tout recommencer depuis le dernier commit.  
  
On a le droit de prendre 2 minutes pour réfléchir, 2 minutes pour refactorer mais si les deux minutes sont passées et que les testes ne passent pas => `reset hard`.  
  
C'est hard...  
  
En pratique, ça donne un binôme survolté, qui fait beaucoup de `reset hard`, qui travaille dans la panique, qui fait tout sauf du beau code et qui, à un moment donné, se dit : *" tiens ? et si on réfléchissait pendant 2 minutes ? "*.  
  
Et là, bouffée d'air, on pense, on conçoit, on adopte une stratégie qui consiste à commiter souvent du code qui marche (des baby steps).  
  
Au final, nous avons opté pour ne pas faire de gros commits de 2 minutes mais plutôt une série de commits de 30s sur les 2 minutes imparties. Et lorsqu'il y avait un gros bout de code à écrire on prenait le temps de réfléchir pendant 2 minutes avant de passer à l'action.  
  
Cette session a été ma préférée, intense, difficile, compétitive, qui nous fait rapidement tomber dans nos travers du quotidien lorsqu'il y a un coup de bourre et révélatrice que, même dans ces moments, on peut faire du bon code en appliquant une stratégie intelligente : diviser pour mieux régner.

## Session 6 : Interdiction de communiquer

![Interdiction de communiquer](/img/GDCR-2016/Silence.jpg)  
  
Dernière et ultime session, le **mute pair-programming** : interdiction de communiquer, que ce soit en parlant, en langue des signes, en écrivant des commentaires ou par tout autre moyen.  
  
La deuxième des quatre règles pour un design simple est reine : **l'intention doit se révéler.**  
  
Dans mon cas ça a été difficile, très difficile, voire franchement pénible. Nous étions en trinôme, et celui qui a commencé a écrit un test que les deux autres n'ont pas compris et nous sommes restés bloqués facilement 15 minutes à... ne rien faire du tout et les 30 minutes restantes à bricoler des trucs sans cohérence.  
  
Il y a plusieurs raisons à cela.  
  
Tout d'abord, alors que dans toutes les autres sessions les règles du **jeu de la vie** ont été testées en premier, ici, celui qui a commencé est parti de l'univers contenant les cellules et, en plus, en traitant un point spécifique sans intérêt particulier.  
  
Ensuite, ni le nom du test, ni le code, n'indiquaient son intention et ce vers quoi il voulait aller.  
  
Et pour finir, même sans communication, il faut une certaine *symbiose* entre les membres de l'équipe, surtout s'ils n'ont que le code pour communiquer.  
  
Ce tout petit test de rien du tout est à l'origine d'un code digne d'envoyer le développeur qui l'a produit dans la cachette de la honte.  
  
Faire comprendre son intention dans le code est peut-être la partie la plus difficile des **quatres règles pour un design simple**.

## Retrospective de la journée

![Retrospective](/img/GDCR-2016/DSC_4111.jpg)  
  
Dans le principe du TDD, il faut écrire un test qui ne marche pas (parce que le code n'est pas encore implémenté) puis implémenter juste ce qu'il faut pour que le test passe (**faire le minimum nécessaire**).  
  
La théorie voulant que, si tous les tests sont faits, alors la solution est implémentée comme attendue et si ce n'est pas le cas c'est qu'il manque des tests.  
  
Dans la pratique, faire qu'un test passe consiste, par exemple, à se contenter de faire un `return true;` dans une méthode sensée contenir un code complexe, tout simplement parce que le test unitaire attend un `true` et, donc, de ne pas implémenter ce qui est attendu, au moins dans un premier temps.  
  
Je demande à voir ce que ça peut donner sur un projet réél, c'est tellement contre-intuitif.  
  
Par contre, commencer par les tests implique de se poser tout de suite la question de comment utiliser le modèle, d'être dans le concret dés le départ et donc de produire un code *utile*.  
  
Le travail en **pair programming** est super intéressant également. On travaille à deux, on augmente nos chances de tout prendre en compte et on est plus efficace à établir un modèle propre et cohérent. En plus, au lieu d'être seul à comprendre ce qu'on a fait, on est deux et la transmission du savoir est facilitée.  
  
Le changement de partenaire à chaque session s'est révélée facile. Il n'y a pas vraiment de temps d'adaptation à l'autre, ça se fait très vite.  
  
Les facilitateurs nous ont ensuite posé 3 questions.

### Qu'est-ce que j'ai appris aujourd'hui ?

Ce qu'est e TDD, que 45 minutes c'est court, mais que prendre le temps de réflechir apporte un niveau de compréhension et une qualité du code qui rattrape largement le fait de ne pas avoir exploiter à 100% ce temps pour du code brut.

### Qu'est-ce qui m'a surpris aujourd'hui ?

D'avoir produit si peu de code en une journée, abstraction faite d'avoir systématiquement supprimer le travail produit.  
  
Et d'avoir malgré tout le sentiment, et la certitude, d'avoir fait le job.

### Que vais-je mettre en application lundi ?

En toute franchise, je ne me souviens plus de ce que j'ai dit que je ferai mais je sais que je ne l'ai pas fait.  
  
Par contre, je vais proposer et travailler avec les équipes pour mettre en place ces pratiques qui seront bénéfiques tant pour les équipes que pour nos clients.

## Conclusion

Chose intéressante lors du retour fait par les facilitateurs, la façon de présenter l'exercice influe la façon dont les participants vont rechercher une implémentation.  
  
L'année dernière, le jeu de la vie avait été expliqué en parlant d'une grille univers dans laquelle évoluaient les cellules et en complétant la description avec les règles du **jeu de la vie**. Et l'année dernière, tout le monde a commencé à créer et tester cet univers en premier.  
  
Cette année, il n'y avait que les règles, l'univers était sous-entendu et nous avons tous commencé par tester les règles en premier.  
  
La façon de présenter les choses peut avoir un impact non négligeable sur la suite et ça me rappelle fortement cette expérience en agilité qui consiste à donner à des groupes distincts la meme spécification. Certains groupes l'ont avec des petits caractères et les autres avec des gros caractères. Ceux qui ont les gros caractères et donc plus de pages estiment une charge plus importante que les groupes avec les petits caractères.  
  
Bref, super expérience. J'essaierai d'y revenir l'année prochaine, il y a plein de choses à découvrir encore. Mais cette fois je préparerai ma machine proprement avec un bootstrap **IDE** + **java** + **Junit** + **Git** pour ne plus perdre de temps à configurer tout ça et me concentrer sur l'exercice.

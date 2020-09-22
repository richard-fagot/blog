---
title: "NanoVNA - Comment créer un DUT holder simple pour la HF"
date: 2020-06-18
tags: 
- Tutoriel
- Radioamateur
- NanoVNA
- DUT Holder
- KiCad
bigimg: [{src: "/img/dut-holder-hf/feature.jpg"}]
math: true
draft: true
---

Il s'agit d'un simple petit bout de PCB avec un connecteur SMA mâle à chaque extrémité desquelles on fait partir deux lignes où l'on pourra fixer notre composant à tester (résistance, condensateur, self, filtre...) grâce à un NanoVNA.

## TL;DR
En fait, si le composant testé n'a pas un Q élevé, dans la bande HF, on peut directement le souder sur un connecteur SMA femelle.

## Prérequis

 - KiCad 5 ;
 - [Plugin RF Tools](https://github.com/easyw/RF-tools-KiCAD) ;
 - [Plugin ViaStitching](https://github.com/jsreynaud/kicad-action-scripts) ;
 - [Librairie d'empreintes personnalisées *SMA_PIN:SMA_EDGE_NRW*](https://github.com/richard-fagot/kicad-footprints).


## Description
C'est un petit bout de PCB, sans composants à l'exception des deux connecteurs SMA et, pourtant, ce n'est pas si évident que cela à concevoir (mais très facile à réaliser).

Comme on travaille dans le domaine fréquentiel de la HF (de 3 à 30 MHz environ) il faut tenir compte des impédances et ne pas introduire de rupture de ces dernières dans notre PCB, en particulier entre les connecteurs SMA et les pistes. 


Les connecteurs SMA ayant une impédance de 50 \\(Omega\\) il faut que les pistes aient la même impédance. 

Il va falloir travailler un petit peu. À ces fréquences, l'impédance des pistes sur le PCB va avoir un impact sur les mesures (\TODO: quel impact, s'évalue à combien, est-ce vraiment significatif ?).

## Le schéma électronique

**\TODO:**

1. Connecteur coaxial
1. Test points
1. Association d'empreinte

## Le PCB

**\TODO:**

### Impédance d'une piste
Une piste de PCB, comme tout conducteur soumis à un courant variable, présente une "résistance" à la variation de courant qu'on appelle impédance. Cette impédance, à une fréquence donnée, va dépendre de la nature du conducteur, de sa géométrie et du milieu qui l'entoure.

Dans notre cas, on va considérer uniquement le PCB sans ses connecteurs. L'impédance d'une piste dépendra de sa largeur, son épaisseur et des plans de masse qui l'entourent.

En général, on passe par un fabricant de PCB 

### Liaison entre le pad des connecteurs et la ligne 50 \\(\Omega\\)
La ligne de 50 \\(\Omega\\) est très grande devant les pads des connecteurs SMA. Si on tire la piste de cuivre jusqu'au centre du pad on arrive presque à toucher les pad de masse du connecteur (cf. figure XXX).

**\TODO: insérer ici l'illustration**



éviter de modifier les empreintes de composants. Il vaut mieux considérer que pour un composant donné il existe une et une seule empreinte de façon à simplifier l'association d'empreinte après la conception du schéma.
Modifier une empreinte implique de se créer une librairie personnelle qu'il ne faudra pas oublier de partager et de correctement documenter si on veut que notre travail soit reproductible. De plus, les composants pouvant évoluer il faudrait également faire évoluer notre librairie personnelle (il arrive que le pinout de certains composants changent). Tout cela devient vite compliqué à gérer.

Pour assurer une bonne transition entre les pads des composants et la piste 50 Ohm d'impédance il existe alors deux solutions :
- soit on crée un symbole qui aura un pad trapézoïdal pour faire la liaison ;
- soit on utilise un plugin RF pour Kicad qui se chargera de faire ce pad à notre place.

Pour le premier cas, rapidement, il faut créer une nouvelle empreinte avec deux pads connectés ayant la même numérotation (deux pads 1). L'un avec la largeur du pad du composant qu'on veut relier à notre piste 50 \\(\Omega\\) et l'autre de la largeur de notre piste. Ensuite, soit on crée également un symbole dédié qu'on fera apparaître dans le schéma et qu'on associe à ce nouveau pad, soit on insère notre empreinte directement dans *PCBnew*.


On va se faciliter la vie et utiliser le plugin :

1. Ouvrir l'éditeur d'empreinte ;
1. Créer une nouvelle librairie RF_PADS ;
1. Créer une nouvelle empreinte ;
1. Cliquer sur le générateur d'empreinte ( puce avec un engrenage) ;
1. Choisir uW...Tamper ;
1. Dans P1 height mettre 1.4 ;
1. Dans P2 height mettre 2.9 ;
1. Sauver l'empreinte dans la librairie RF_PADS ;
1. Retourner dans PCBNew ;
1. Cliquer sur ajouter une empreinte ;
1. Sélectionner notre nouvelle empreinte ;
1. sélectionner le plus petit pad de cette empreinte, paramètre, choisir le net du premier connecteur ;
1. sélectionner le plus grand pad de cette empreinte, paramètre, choisir le net du premier connecteur ;
1. Ajouter une seconde empreinte et recommencer les deux étapes précédentes en choisissant le net du second connecteur ;
1. Positionner, router.

## Conclusion
Ce genre de DUT Holder, en fait, n'est pas du tout utile pour ce genre de mesure. On peut obtenir les mêmes résultats en soudant le composant étudié directement sur un connecteur SMA femelle.

**\TODO: insérer ici illustration du composant soudé sur le SMA et connecté au NanoVNA avec les courbes obtenues comparées à celles réalisées précédemment.**

Par contre, pour des composants avec un Q élevé (quartz, filtres à quartz, filtres céramiques...) un DUT Holder dont on connait parfaitement le plan de référence, le point "zéro" de la phase et qui a une continuité d'impédance impeccable est essentielle. Et c'est d'autant plus vrai dans les fréquences plus importantes que la HF.
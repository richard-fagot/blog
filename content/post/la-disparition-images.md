---
title: "AngularJS, mobile et disparition d'image."
date: 2016-03-11
tags: 
- Angular
- "Opérateur mobile"
- Images
description: "Chez certains opérateurs mobile, les images ne s'affichent pas avec AngularJS."
---

Une application web mobile en **AngularJS**, des images qui tantôt s'affichent sur certains mobiles, tantôt pas. La disparition de ces images n'est pas mystérieuse ni aléatoire mais est causée par des êtres se dissimulant dans les profondeurs obscures du réseau et laissant leur trace dans nos applications développées avec force et courage.

## TL,DR

1. Utilisez la directive `ng-src` pour indiquer l'emplacement relatif de vos images ;
2. Fin.

## Le contexte

Pour un client, nous avons développé une application **AngularJS** avec Bootstrap pour une utilisation sur mobile en 3G/4G.  
  
Lors des tests, il s'est trouvé des cas où les images n'apparaissaient pas et, après investigation, seuls les utilisateurs sous certains opérateurs en 3G étaient concernés.

## La raison du problème
Certains opérateurs effectuent des manipulations des ressources téléchargées avant des les envoyer au navigateur.  
  
Par exemple, il est assez courant que les images soient recompressées, donnant, au passage, [des résultats parfois franchement dégradés](http://www.hteumeuleu.fr/la-compression-dimages-par-les-operateurs/).  
  
Parfois, les opérateurs vont plus loin et modifient le code source de la page HTML elle-même. Et, dans notre cas, ils passent sur les attributs `src` et remplacent les urls en chemin relatif par une url en chemin absolu à partir de l'url du fichier HTML lu.  
  
Dans le cas d'**AngularJS**, les différentes vues de l'application sont distribuées dans des fichiers HTML possédant une arborescence propre et éloignée de la racine ou se trouve le *index.html*.  
  
**AngularJS** gère très bien ces urls relatives à la racine de l'application même si elles sont écrite dans une sous-arborescence. C'est précisément ce qu'on lui demande.  
  
Le problème est que l'opérateur remplace la valeur des attributs `src` en chemin relatif avant le passage d'**AngularJS** par des url en chemin absolu en partant de l'emplacement du fichier HTML qui les contient.  
  
On se retrouve donc avec des :  
  
`http://context/app/component/vue/app/assets/images/mon_image.png`  
  
au lieu de :  
  
`http://context/app/assets/images/mon_image.png`


## La solution

La solution est simple, il suffit d'utiliser systématiquement la directive `ng-src`.  
  
Les opérateurs ne savent pas les traiter et les laissent tels quels, ce qui permet à **AngularJS** de faire son travail correctement et d'afficher les images.  
  
Un second avantage est que dans **Angular 2**, il est fortement recommandé d'utiliser cette directive, ce qui permet, d'ors et déjà, de prendre de bonnes habitudes.  
  
Le projet d'exemple se trouve sur <https://github.com/richard-fagot/rfd-disparition> et on peut le tester en live sur <http://richard-fagot.github.io/rfd-disparition/>.

## Corollaire

Ce problème de parasitage de l'opérateur complexifie encore plus la phase de test des applications web mobiles : non seulement il faut tester l'application sur différents modèles de téléphones et tablettes, d'OS et de navigateurs mais, en plus, il faut tester sur différents opérateurs et réseaux (3G, 4G, etc.).  
  
Dans notre cas, les images étaient absentes pour un opérateur bien connu en 3G seulement (en 4G ça marchait correctement) et pour un opérateur virtuel reposant sur le réseau d'un autre opérateur physique que le premier et en 3G également.



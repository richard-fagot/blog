---
title: Rainbow Lightpainting
subtitle: Fabrication d'un bâton lumineux arc-en-ciel multimode
date: 2020-04-28T19:05:46+02:00
draft: true
math: true
---

Dans l'école de mes enfants, l'ALAE est super dynamique et porpose tout plein d'activités géniales pour les enfants.
En discutant avec une animatrice je parlais de ma passion pour la photo et ça commençait à l'inspirer pour monter une nouvelle activité jusqu'à ce que j'évoque le lightpainting. Ça lui a tout de suite plu et elle s’est approprié la technique et a monté une nouvelle activité au sein de l’ALAE. Je lui prête l’essentiel du matériel et elle a permis aux enfants de faire des photos extra avec ces petits bout’choux.

Les outils dont elle dispose sont essentiellement des petites lampes torches sur lesquelles on a scotché des filtres colorés. Rien qu’avec ça ils font déjà des supers trucs mais j’avais envi de leur permettre de varier encore plus leurs créations. C’est là que m’est venue l’idée d’un bâton de lumière qui permettrait de faire des drapés colorés.

## Fournitures
  
1. Un tube plastique transparent diamètre intérieur 35 mm. longueur XX cm ;
1. 20 LEDs RGB haute luminosité boitier 5 mm opaque à cathode commune ;
1. 40 résistances 100 \\( \Omega \\) ;
1. 20 résistances 150 \\( \Omega \\) ;
1. 1 ATTiny85 ;
1. 1 support lyre 8 broches ;
1. 3 Transistors 2N2222A ;
1. 3 résistances XX \\( \Omega \\) ;
1. Un arduino pour programmer le ATTiny85 (le Uno par exemple) ;
1. 4 longueurs de 64 cm de fil de laiton diamètre 0.8 mm ;
1. Un fer à souder ;
1. De l'étain ;
1. Du flux ;
1. Une plaque d'epoxy de XX x XX mm ;
1. Une perçeuse type Dremel avec un forêt de XX mm ;
1. Une imprimante 3D avec du PLA ;
1. Une imprimante laser ;
1. Des vis longueur XX diamètre XX ;
1. [Facultatif] Les différents moules d'assemblage ;

## Présentation du bâton lumineux
Le bâton lumineux se présente sous la forme d'un « sabre laser » d’une soixantaine de centimètres de long (hors manche) qui peut soit afficher une couleur fixe soit varier de couleur (effet *arc-en-ciel*). 

Le mode couleur fixe permet de créer des drapés monochrome. En appuyant sur le bouton de sélection du mode une fois on sélectionne la couleur désirée en tournant le potentiomètre. Un second appui sur le bouton permet de régler la luminosité avec ce même potentiomètre.

Le mode  *arc-en-ciel* permet de créer des drapés dont la couleur change le long du mouvement. En appuyant sur le bouton de sélection du mode une fois on contrôle la vitesse de variation en tournant le potentiomètre. Un second appui sur le bouton permet de régler la luminosité comme pour le mode couleur fixe.

À la mise en route du bâton lumineur on se trouve dans le mode *arc-en-ciel* et on peut contrôler la vitesse de variation des couleurs.

**Ajouter un petit graphique expliquant le passage entre les modes**
 

## Étape 2 : Partie électronique
L’ATTiny85 est un super petit microcontrolleur. Il dispose de 6 broches d’entrée/sortie et d’une mémoire bien suffisante pour le programme, il peut tourner à 8 MHz (c’est ultra rapide pour un petit programme comme celui-ci), il est facilement programmable avec un arduino et il est vraiment bon marché.

![ATTiny85 pinout](/img/)
Pour limiter le nombre de composants électronique j’ai choisi de contrôler la luminosité des leds par PWM (et non par le courant). Du coup, il faut choisir avec soins les broches de l’ATTiny car toutes ne proposent pas cette fonction.

Pour faire ce bâton lumineux il nous faut des leds RGBs, ici à cathode commune (la masse en commun). Chaque couleur est contrôlée par une broche dédiée sur la led.
Nous avons également besoin d'un bouton poussoir pour pouvoir changer de mode (une broche) ainsi qu'un potentiomètre pour faire varier 

Le schéma électronique et le typon ont été conçus avec [EasyEDA](https://easyeda.com/).
Pour réaliser ce projet j'ai cherché un composant programmable, petit et bon marché. Comme j'ai l'habitude de travailler avec les arduinos 

## Étape 3 : Programmation de l’ATTiny85
## Étape 4 : Soudure des composants
## Étape 5 : Soudure des LEDs
## Étape 1 : Impression 3D du manche
## Étape 6 : Assemblage et mise en route







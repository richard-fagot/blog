---
title: "SDR - Décoder le mode FT8 facilement sous windows"
date: 2020-06-18
tags: 
- Tutoriel
- Radioamateur
- FT8
- pskrecorder
- SDR
- WSJT-X
- Cubic SDR
bigimg: [{src: "/img/ft8-windows/feature.jpg"}]
math: true
---

Le FT8 est un digimode créé par K1JT pour réaliser des contacts (QSO) sur de très longues distances avec très peu d'énergie. Devenu extrêmement populaire il est courant de pouvoir faire des contacts avec des gens habitants de l'autre côté de la terre.

## Prérequis
Pour ce tutoriel il vous faut posséder une antenne, si possible centrée sur la fréquence que vous souhaitez écouter (mais un long fil planté dans votre clé ça marche bien aussi), ainsi qu'une clé RTL-SDR installée. 

## Logiciels nécessaires
- [Cubic SDR](https://cubicsdr.com/?cat=4) (pour écouter ce qui vient de la clé RTL-SDR) ;
- [WSJT-X](https://physics.princeton.edu/pulsar/K1JT/wsjtx.html) (pour décoder le mode FT8) ;
- [Virtual Audio Cable](https://www.vb-audio.com/Cable/) (pour rediriger le son venant de cubic SDR vers WSJT-X).


## Installation
### Cubic SDR
L'installation de *Cubic SDR* est simplissime : après avoir téléchargé l'installeur il suffit de double-cliquer dessus et de suivre les instructions.

### WSJT-X
L'installation de *WSJT-X* est aussi simple : on double-clique sur l'installeur après l'avoir télécharger et on se laisse guider.

### Virtual Audio Cable
*Virtual Audio Cable* est presque aussi facile à installer car il y a une petite subtilité. Après avoir téléchargé le fichier il faut le dézipper (dans le répertoire de téléchargement c'est très bien). Ensuite, il faut aller dans le répertoire dézippé et faire un clic droit sur le fichier *VBCABLE_Setup_x64.exe* et sélectionner *Exécuter en tant qu'administrateur*.

![Exécuter en tant qu'administrateur](/img/ft8-windows/admin.png)

Confirmez et poursuivez l'installation.

Maintenant vous pouvez redémarrer Windows 10 pour bien prendre en compte cette installation.

## Mise en route
Commencer par lancer *Cubic SDR*. Au démarrage il demande de sélectionner la clé RTL-SDR. Sélectionner-là.

![Sélection de la clé RTL-SDR](/img/ft8-windows/choix-cle.png)

Sélectionner le mode *USB* puis une des fréquences suivantes (non exhautive). 



| Bande   | Fréquence     |
| ------- |:-------------:|
| 160m    |  1.840 Mhz    |
| 80m     |  3.573 Mhz    |
| 60m     |  5.357 Mhz    |
| 40m     |  7.074 Mhz    |
| 30m     |  10.136 Mhz   |
| 20m     |  14.074 Mhz   |
| 17m     |  18.100 Mhz   |
| 15m     |  21.074 Mhz   |
| 12m     |  24.915 Mhz   |
| 10m     |  28.074 Mhz   |
| 6m      | 50.313 Mhz    |
| 4m      | 70.095 Mhz    |
| 2m      | 144.174 Mhz   |


Attention, selon le type de clé toutes les fréquences ne sont pas disponibles : pour les clés RTL-SDR bon marché, il n'est pas rare que les fréquences sous les 60 MHz ne soient pas accessibles (pour les écouter il faut utiliser un *upconverter*). 

Il peut également y avoir un petit décalage de fréquence due à l'imprécision de la clé RTL-SDR. Dans ce cas centrez bien la largeur de bande sur le signal reçu.

![Sélection du mode et de la fréquence](/img/ft8-windows/selection-freq-mode2.png)

Si la réception est bonne vous devez voir apparaître dans le waterfall un signal qui ressemble à ça :

![Exemple de signal FT8](/img/ft8-windows/waterfall-exemple.png)


Maintenant nous allons rediriger le signal sonnore généré par *Cubic SDR* (celui qu'on entend sur les hauts-parleurs) dans le câble audio virtuel. 

Pour cela :
1. Cliquer sur l'icône son de la barre des tâches ;

![Paramètre son](/img/ft8-windows/parametres-son.png)

2. Cliquer sur le nom de la sortie son par défaut ;

![Accès sélection sortie](/img/ft8-windows/parametrage-sortie-son.png)

3. Sélectionner *CABLE input (VB-Audio Virtual Cable)*.

![Sélection câble virtuel](/img/ft8-windows/selection-cable-virtuel.png)

Vous n'entendez plus rien et c'est normal car le son est redirigé vers une sortie virtuelle que nous allons utiliser en entrée de WSJT-X.

Justement, il est temps de lancer WSJT-X. Une fois ouvert aller dans ***File > Settings…***

![WSJT-X Settings](/img/ft8-windows/settings.png)

Ouvrir l'onglet ***Audio*** et dans le champ ***input*** sélectionner le câble audio virtuel puis cliquer sur ***OK***.

![Sélection entrée son](/img/ft8-windows/selection-entree-son.png)

Ensuite, configurer le mode de décodage FT8 dans ***Mode > FT8***.

![Sélection du mode FT8](/img/ft8-windows/selection-mode-ft8.png)


Enfin, sélectionner la bande de fréquence choisie. patienter entre 15 et 30s et les premiers décodages devraient apparaître.

![Décodage en cours](/img/ft8-windows/decodage-FT8.png)


## Pour aller plus loin
Toutes les écoutes établies avec WSJT-X peuvent être visualisées sur une carte du monde. Cela permet de mieux se rendre compte d'où viennent les signaux que l'on a reçu, et ils peuvent venir de très loin.

Pour cela on va s'appuyer sur les services de *PSKReporter* mais avant il vous faut un indicatif d'écouteur (rien d'obligatoire en 2020 mais je vous le conseille, on attrappe vite le virus) et connaître votre *locator*.

Pour l'indicatif il y a plusieurs associations qui en distribuent gratuitement. Le site de [F-10255](https://f-10255.pagesperso-orange.fr/identifiants/identifiants.htm) en parle bien et donne plusieurs liens où faire sa demande d'indicatif.

Pour le *locator* c'est un identifiant qui permet de localiser dans un rectangle votre poste d'écoute sur la planète, un peu comme des coordonnées GPS, mais en moins précis. Il suffit d'aller [sur ce site](http://www.egloff.eu/googlemap_v3/carto.php) et de zoomer là où vous écoutez. Au plus on zoom et au plus les coordonnées obtenues sont précises, vous pouvez vous arrêter à 2 lettres, 2 chiffres et 2 lettres.

Une fois votre indicatif SWL (d'écouteur) et votre *locator* en main il vous suffit de les renseigner dans les champs ***My call*** (indicatif SWL) et ***My grid*** (le locator) dans ***File > Settings… > General*** puis de cocher ***Enable PSK Reporter Spotting*** dans l'onglet ***Reporting***.

Quelques minutes plus tard, tous les signaux reçus apparaîtront sur le site de [PSK Reporter](https://pskreporter.info/pskmap.html) en saisissant votre indicatif dans le champ de recherche.

![PSK Reporter](/img/ft8-windows/feature.jpg)

**Amusez-vous bien et bonne écoute !**

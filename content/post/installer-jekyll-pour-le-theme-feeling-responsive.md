---
title: "Installer Jekyll pour faire tourner le thème Feeling Responsive"
date: 2015-08-13
tags: 
- ubuntu
- jekyll
- feeling responsive
---
Installer Jekyll sous ubuntu 14.04 n'est pas trivial : les dépôts contiennent une version d'outre-tombe de Jekyll et une version poussiéreuse de Ruby. En plus, Jekyll seul ne suffit pas, il faut en plus installer nodejs.  
  

Plutôt que d'avoir une gueule de revenant après avoir chercher pendant des heures comment faire tourner le bouzin, faites ceci :  
  

{{< highlight sh>}}
apt-add-repository ppa:brightbox/ruby-ng
apt-get update
apt-get install ruby2.2 ruby2.2-dev
apt-get install nodejs npm
gem install jekyll
{{< / highlight>}}
 
Youpi, c'est fini et vous avez gardé votre physique de jeune premier !
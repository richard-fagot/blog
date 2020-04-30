---
title: "Installer une clé SSH pour github sous ubuntu 14.04"
date: 2015-08-12
tags: 
    - ubuntu
    - github
    - ssh
---

1. Suivre les étapes [indiquées dans Github](https://help.github.com/articles/generating-ssh-keys) sans faire la 5 ;
2. Faire `ssh-keyscan -t rsa github.com > ~/.ssh/known_hosts` ;
3. Faire l'étape 5 ;
4. cloner le projet git en utilisant le clone SSH.
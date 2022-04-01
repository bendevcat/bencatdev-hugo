---
author: "benCat"
title: "Docker: Gestion du PID 1 avec Tini"
date: "2021-08-20"
description: "Ou comment remettre de l'ordre dans ton conteneur !"
tags:
  - "docker"
categories:
  - "DevOps"
image: "cloud-background.png"
---

# UN PEU D'HISTOIRE

Dans des temps oubliés, le déploiement d'une application finissait irrémédiablement sur un serveur (physique ou virtuel).
Lors du lancement de votre instance, l'OS créer un nouveau processus, et lui attribue un numéro de PID (Process IDentifier) unique afin de pouvoir identifier ce processus par la suite.

Le premier processus lancé se voit attribuer le PID numéro 1, les prochains se retrouvent incrémentés.

Sous Linux, le PID 1 n'est autre que le processus "init", qui sert à initialiser le système.

# THE DOCKER WAY

Lors du lancement d'un conteneur Docker, celui-ci utilise l'ENTRYPOINT ou la CMD finale de l'image, en tant que PID 1.

Par exemple, si je créé un conteneur à partir d'un Dockerfile qui lance une application Node avec 'CMD ["npm", "start"]', le PID 1 sera attribué à 'npm'.

Ce qui pose quelques problèmes : La gestion des 'child processes' n'est pas intégrée, des zombies peuvent apparaître (pour X raisons), les signaux envoyés par votre application (comme SIGTERM) ne seront plus interprétés... bref, le conteneur devient bordélique, et il ne reste plus qu'à le reboot pour repartir sur une base saine, qui finira elle aussi par partir en vrille.

# TINI - A TINY BUT VALID INIT FOR CONTAINERS

C'est là que Tini entre en jeu : il va s'occuper de votre PID 1 et faire tout ce qu'un init sait faire !

Fini les zombies, fini les signaux non reçu, bonjour les conteneurs sains !

## UTILISATION

C'est aussi simple que d'ajouter ceci dans votre Dockerfile :

```dockerfile
ENV TINI_VERSION v0.19.0
ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /tini
RUN chmod +x /tini

ENTRYPOINT ["/tini", "--"]

CMD ["npm", "start"]
```

et c'est tout !
Aucun autre changement n'est requis : si votre conteneur démarre correctement sans Tini, il en sera de même avec ;)

## VA CHERCHER BONHEUR

Voici un lien vers le repo du projet : https://github.com/krallin/tini

Le README est bien fourni, vous trouverez tous les détails dont vous avez besoin pour le mettre en place !
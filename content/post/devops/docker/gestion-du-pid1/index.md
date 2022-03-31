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

Lors du lancement d'un conteneur Docker, celui-ci
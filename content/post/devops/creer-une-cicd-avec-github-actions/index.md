---
author: "benCat"
title: "Créer une CI/CD complète avec Github Actions"
date: "2022-04-01"
description: "Construisez une automatisation facilement et à moindre frais !"
tags:
  - "docker"
categories:
  - "DevOps"
image: "cloud-background.png"
---

# LE BUT

## POURQUOI GITHUB ACTIONS ?

Un besoin de monter une nouvelle CI pour remplacer Jenkins X v2, qui devenait très instable et déprécié, rapidement.

Mon entreprise à une souscription Github qui nous "offre" 50 000 minutes sur Actions, un petit POC s'est donc imposé.

## POURQUOI FAIRE ?

L'objectif était simple :
- Faire tourner lint + tu
- Construire l'image Docker
- La pousser sur un registry

2 heures plus tard, mon POC faisait le job !

Alors bien sûr, c'était crade, les actions étaient prises un peu au hasard, mais mes besoins étaient remplis, je pouvais donc passer à la suite.

## C'EST TOUT ?

Mais avant ça, pourquoi ne pas pousser le concept un peu plus loin, avec une CD ?

Mes besoins, dans les grandes lignes :
- Récupérer les infos du build
- Mettre à jour le chart Helm du service
- Déployer le chart sur un cluster Kubernetes
- Envoyer une notification Teams pour rendre compte de l'update

C'est à ce moment là que j'ai posé le stylo et que j'ai bouffé la documentation d'Actions.

# LA PRATIQUE

## HELLO-WORLD

> en cours de rédaction
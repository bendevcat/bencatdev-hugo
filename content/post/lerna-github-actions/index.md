+++
draft: true
author = "benCat"
title = "Lerna avec Github Actions"
date = "2021-08-25"
description = "Comment mettre en place une CICD avec Actions sur un monorepo Lerna 'independent'"
tags = [
    "devops",
    "cicd",
    "actions",
]
categories = [
    "tutoriel",
]
#aliases = ["migrate-from-jekyl"]
image = "lerna-monorepo.png"
+++

J'ai eu à mettre en place une CICD sur un monorepo Lerna.
Je connaissais le principe mais je n'avais jamais eu l'occasion de bosser avec, j'ai donc forcement galéré pour arriver à remplir la checklist de mon lead-tech.

## LA CHECKLIST

Voici les pré-requis pour ce poc :
- Lerna doit fonctionner en mode 'independent'
- La gestion des versions doit donc être indépendante
- Un changelog paramétrable doit être généré à chaque build
- Un pull d'un repo NPM privé doit être possible
- Tout merge sur master doit publier la/les librairie/s sur Github Package et NPM

---
title: "Mon alternance"
date: 2025-08-17 21:16:00 +0200
categories: [dev]
tags: [golang, vueJS, web, frontend, backend]
---

## Introduction

Dans ce poste je parlerai de mon travail en alternance, je parlerai des technologies que j'ai l'occasion d'utiliser ainsi que des technologies que j'ai pu apprendre.

Je suis actuellement développeur logiciel en alternance chez Alcatel Lucent Enterprise, je travaille sur différentes technologies, notamment du web et du mobile.

## Technologies

- **Golang** : backend pour les projets web
- **VueJS** : frontend pour les projets web
- **React Native** : application mobile pour un des services d'Alcatel
- **Docker** : conteneurisation des projets et déploiement multi-plateforme
- **Ansible** : automatisation de configuration de machines et de pods Kubernetes

### Un projet : [Data Transfer Server](https://github.com/0x-Saegor/data-transfer-server)

Ce projet réalisé comme mini-projet d'introduction dans l'entreprise m'a permis d'apprendre Golang et VueJS. J'ai découvert ces deux technologies et me suis formé pendant plusieurs jours avant de me mettre à 100% dans le développement de l'application web.

<object data="{{ site.url }}{{ site.baseurl }}/pdfs/Subject.pdf#toolbar=0" width="100%" height="400" type="application/pdf"></object>

L'objectif étant d'envoyer des paquets de taille connue entre le serveur et le client pour s'assurer de la fiabilité du tracker sur les switchs.
Grâce au Golang j'ai mis en place le backend, celui ci fonctionne avec un serveur web Gin qui permet de fournir le frontend et de fournir des endpoints API à appeler.

L'appel aux endpoints permet le téléchargement et l'upload de fichiers. Le frontend se charge d'afficher des barres de chargement et de permettre différentes actions de téléchargement / upload prédéfinies (1MB, 10MB, 100MB).
Le frontend est en VueJS, connaissant ReactJS au préalable j'ai apprécié découvrir Vue qui suit un chemin similaire mais avec une approche différente.

Une fois le projet terminé je devais le déployer, pour cela j'ai utilisé Docker. Grâce à un Dockerfile j'ai déployé l'image docker parfaitement fonctionnelle sur un cluster Kubernetes.

### Mes autres activités

##### **OVTX**

Développement d'un panneau de configuration pour une solutions d'Alcatel, je fais du VueJS pour le front, du Go pour le back et j'utilise Ansible pour déployer automatiquement les modifications effectuées au DNS, DHCP et NTP sur toutes nos machines.

Ansible nous permet également de déployer automatiquement sur toutes les machines notre backend buildé et de relancer les services pour qu'il soit lancé. Nous avons prévu un système de Rollback en cas d'erreur lors du déploiement et un système de vérifications de checksum pour s'assurer qu'il y a une modification : s'il n'y en a pas il est inutile d'envoyer le fichier sur le serveur.

##### **AssetTracking**

Maintenance du service AssetTracking, fix de bugs sur le frontend, le mobile et le backend, mise à jour des paquets.
Le frontend est en VueJS avec un backend en JS (avec sails).

Pour ce projet j'ai eu l'occasion de me former à React Native, l'application mobile fonctionnant entièrement sous cette techno.

---
title: "Gamehacking Journey : mon apprentissage du reverse de jeux"
date: 2026-03-22 14:00:00 +0100
categories: [dev]
tags: [cpp, reverse-engineering, gamehacking, windows]
---

Je suis tombé sur un dépôt très intéressant : [Gamehacking-Journey](https://github.com/0x-Saegor/Gamehacking-Journey), qui documente un parcours pratique autour du game hacking et de la rétro-ingénierie.

L'objectif du projet est clair : comprendre comment un jeu fonctionne en mémoire, puis implémenter plusieurs techniques en C++ pour observer, modifier et détourner certains comportements en temps réel.

## Le contexte d'apprentissage

Le parcours s'appuie sur les contenus de [Game Hacking Academy](https://gamehacking.academy/) et utilise des outils classiques du reverse :

- **Cheat Engine** pour trouver des valeurs et remonter des pointeurs.
- **x64dbg/x32dbg** pour analyser l'assembleur et poser des breakpoints.
- **Visual Studio + C++** pour coder des exécutables et des DLL.

Ce que j'aime dans cette approche, c'est le côté progressif : on part de manipulations mémoire relativement simples, puis on va vers des hooks plus avancés.

## Les différentes étapes du repo

Le dépôt est organisé par modules, chacun avec son propre README.

### 1) External Memory Hack

Premier niveau : un programme externe lit/écrit la mémoire d'un processus cible avec les APIs Windows (`OpenProcess`, `ReadProcessMemory`, `WriteProcessMemory`).

C'est une bonne porte d'entrée pour comprendre :

- la relation entre adresse de base et offsets,
- la différence entre valeur statique et adresse dynamique,
- la chaîne de pointeurs (pointer chain).

### 2) Internal Memory Hack

Ensuite, on passe en **interne** via une DLL injectée dans le processus du jeu.

L'avantage :

- on manipule la mémoire "depuis l'intérieur",
- on réutilise la base + offsets plus facilement,
- on comprend mieux le cycle de vie d'une DLL (`DllMain`, `DLL_PROCESS_ATTACH`, thread injecté).

### 3) CodeCaveDLL

Partie très instructive : la mise en place d'une **Code Cave**.

L'idée est de rediriger le flot d'exécution vers un bloc de code personnalisé, puis de revenir proprement au code original. On voit bien les notions importantes :

- patch d'instructions avec un `JMP`,
- calcul d'offset relatif,
- sauvegarde/restauration des registres (`pushad`/`popad`),
- précautions pour ne pas casser l'exécution du jeu.

### 4) WallhackMemory

Ici, on applique la logique de hook à l'affichage : modification de valeurs liées à la profondeur pour rendre des entités visibles à travers les murs.

C'est un bon exemple de transition entre :

- reverse "mémoire brute",
- compréhension du pipeline de rendu,
- tuning d'une valeur pour un effet visuel concret.

### 5) WallhackOpenGL

Dernier niveau présenté : interception de fonctions OpenGL (notamment `glDrawElements`) pour agir directement sur le rendu.

Cette approche est plus avancée car elle demande de :

- attendre le chargement de `opengl32.dll`,
- récupérer les adresses des fonctions via `GetProcAddress`,
- installer un hook sur la fonction cible,
- filtrer certains objets selon des critères (exemple : nombre d'arêtes).

## Pourquoi ce projet est intéressant

Ce repo est une bonne base pour apprendre le reverse de façon structurée, car il combine :

- de la théorie (assembleur, mémoire, appels système),
- de la pratique (code C++ concret, modules séparés),
- de la documentation (README dédiés avec explications et captures).

C'est aussi un bon rappel qu'en sécurité, comprendre les techniques offensives permet souvent de mieux concevoir des défenses.

## La suite

Je vais continuer à développer le projet et ajouter du contenu à ma base de connaissances en reverse.
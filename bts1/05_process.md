---
title: Gestion de processus sous Linux
layout: folder
---

## Concepts

Processus: suite d'opérations en cours d'exécution.

Informations associées à un processus sous Linux:
- un numéro d'identification (PID)
- une commande associée et sa ligne de commande
- un dossier de travail
- un compte propriétaire
- le numéro d'identification du processus parent (PPID)
- ...

## Commandes

Plusieurs commandes permettent de connaître et de manipuler les processus
sur le système:

- pstree: permet l'avoir une vision arborescente des processuses
- ps: permet d'afficher des informations sur les processuses
- kill: permet d'envoyer des signaux aux processuses
- renice: change la priorité d'exécution des processuses
- top: affiche en temps réel les ressources utilisées par les processuses

## Le dossier /proc

Linux met à disposition un dossier virtuel dans lequel nous pouvons
retrouver des informations sur le système en cours: /proc

Dans ce dossier, tous les sous-dossiers dont le nom est un nombre
regroupent des informations sur les processuses.

## Pratique

Ici, quelques cheminements permettront de comprendre les différents
concepts:

1. Exécuter et interpréter la sortie de la commande:

  ~~~bash
  $ pstree
  ~~~

2. Explorer la commande ps:

  1. Exécuter `ps` sans argument

  2. Exécuter:

    ~~~bash
    $ ps a
    ~~~

    Affiche tous les processuses de l'utilisateur.

  3. Exemple de ligne fréquente:
    
    ~~~bash
    $ ps auxw | less
    ~~~

    Affiche page par page les processuses de tout le monde.

3. Le processus du Shell

  Dans un terminal, taper:

  ~~~bash
  $ echo $$
  ~~~

  Le résultat est le numéro de processus du Shell en cours

  1. Explorer le dossier `/proc/<PID>`, `<PID>` étant le résultat de la
     commande précédente

  2. Dans ce dossier, constater le résultat de la ligne de commande:

    ~~~bash
    $ ls -l exe
    ~~~


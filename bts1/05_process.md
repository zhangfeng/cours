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

   ```bash
   $ pstree
   ```

2. Explorer la commande ps:

   1. Exécuter `ps` sans argument

   2. Exécuter:

      ```bash
      $ ps a
      ```

      Affiche tous les processuses de l'utilisateur.

   3. Exemple de ligne fréquente:
    
      ```bash
      $ ps auxw | less
      ```

      Affiche page par page les processuses de tout le monde.

3. Le processus du Shell

  Dans un terminal, taper:

  ```bash
  $ echo $$
  ```

  Le résultat est le numéro de processus du Shell en cours

  1. Explorer le dossier `/proc/<PID>`, `<PID>` étant le résultat de la
     commande précédente

  2. Dans ce dossier, constater le résultat de la ligne de commande:

     ```bash
     $ ls -l exe
     ```

## Gestion de job

Les Shells évolués tels que `bash` propose une gestion de "job" qui sont
des processuses "gérables" par l'utilisateur.

Un job n'est ni plus ni moins qu'un processuses mis en arrière-plan de
manière à ce que l'utilisateur puisse le rappeler.

Concepts:

- premier plan: le processus en premier plan est celui avec lequel
  interagit directement l'utilisateur
- arrière plan: un processus en arrière plan est un processus dont
  l'interface n'est pas visible par l'utilisateur. L'utilisateur ne peut
  que lui envoyer des signaux via la commande `kill`.

Les Shells avancés proposent des commandes pour interagir avec les
processuses mis en arrière plan par l'utilisateur.

Un processus mis en arrière plan n'est contrôlable qu'à partir du Shell qui
l'a lan'é.

## Pratique

1. Mis en arrière plan:

   1. Lancer un éditeur avec la commande suivante:

      ```bash
      $ nano premier
      ```

      `nano` se lance avec un fichier vierge

   2. Mettre en arrière plan en appuyant sur la combinaison `CTRL Z`

      Nous sommes sorti de `nano` mais il est encore actif.

   3. Dans le Shell, lister les jobs en tapant:

      ```bash
      $ jobs
      ```

      Nous voyons que `nano` est en arrière plan avec le status **stoppé**.

   4. Remettre `nano` en premier plan:

      ```bash
      $ fg
      ```

      Réapparition de `nano`

   5. On quitte `nano` avec la combinaison `CTRL X`

2. Bascule entre plusieurs jobs

   1. Lancer `nano`:

      ```bash
      $ nano premier
      ```

   2. Passer `nano` en arrière plan

   3. Ouvrir la page `man` de `bash`:

      ```bash
      $ man bash
      ```

      Le `man` est bien affiché.

   4. Passer le `man` en arrière plan avec `CTRL Z`

      Le Shell se réaffiche.

   5. Lister les jobs:

      ```bash
      $ jobs
      ```

      Remarquons les particularités suivantes:

      - il y a bien une ligne par job
      - chaque job possède un numéro noté entre crochets `[` `]`
      - un des jobs est marqué du signe `+` et l'autre du signe `-`

      Le job marqué du signe `+` est le dernier avec lequel on a interagi
      et le `-` est l'avant-dernier.

   6. Nous pouvons revenir sur n'importe quel job avec la commande
      `fg %<numjob>`

      ```bash
      $ fg %1
      ```

      Réapparition de `nano`.

   7. Après avoir passé encore en arrière plan, nous pouvons expérimenter
      comment passer en premier plan le job **précédent**:

      ```bash
      $ fg -
      ```

   8. Une fois expérimenté, faire en sorte de tout bien refermer et
      vérifier que la liste des jobs est vide

3. Expérimenter comme dans l'exercice précédent en ouvrant, cette fois-ci,
   trois jobs

4. Envoi d'un signal:

   1. Ouvrir une page `man`:

      ```bash
      $ man bash
      ```

   2. Passer le `man` en arrière plan

   3. Envoyer le signal `9` sur le job:
      
      ```bash
      $ kill -9 %1
      ```

   4. Constat que la liste des jobs est vide



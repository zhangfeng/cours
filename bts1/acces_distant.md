---
title: Accès distant
layout: bts1
---

## Concepts et généralité

L'accès distant dans ce cours se résumera à un accès de la ligne de
commande sur un serveur Linux.

L'idée est de pouvoir exécuter une commande à distance sur un
serveur. Lancer un Shell n'est qu'un cas particulier.

## Authentification par clé

Exercices à pratiquer:

1. Générer une paire de clé (publique et privée). Utiliser la commande
   `ssh-keygen`

2. Envoi de la clé publique de manière manuelle (dans le fichier
   `.ssh/authorized_keys` du compte destinataire)

3. Envoi de la clé publique vers le serveur avec la commande `ssh-copy-id`

4. Tester un accès simple au serveur et vérifier que ça marche bien avec la
   commande `ssh`

## Shell

Lorsqu'on se connecte avec `ssh` sans donner de commande, un Shell de
connexion est lancé et on se trouve dans le répertoire personnel du compte
(le `home directory`).

Quelques exercices de pratique:

1. Lister le contenu du `home directory`
2. Lister le contenu du dossier `/bin` et `/usr/bin`
3. Un dossier temporaire:
   1. Créer dans le `home directory` un dossier nommé `tmp`
   2. Copier le contenu de `/usr/bin` dans le dossier que l'on vient de
      créer
   3. Vérifier que le dossier contient bien ce qu'on a copié
   4. Effacer le dossier `tmp`
4. Faire une synthèse de la structure de l'arborescence du système (lire la
   page man `hier(7)`)

## Exécution distante

Avec la commande `ssh`, il est possible de lancer une commande et ne pas
rester connecter: `ssh utilisateur@machine commande ARGS...`

Refaire les exercices 1 à 3 dans ce mode là.

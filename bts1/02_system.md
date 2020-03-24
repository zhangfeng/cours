---
title: Système Unix / Linux
layout: folder
permalink: bts1/system
---

Proposition de définitions:

- Système d'exploitation: une trousse à outil permettant d'utiliser
  (d'exploiter) un ordinateur
- Logiciel: ensemble de programmes assemblés autour d'une problématique
- Interface: ce qui permet d'interagir avec un logiciel ou le système

## Structure de l'arborescence des fichiers Linux

Linux est un système faisant partie de la famille Unix. Toute cette famille
suit des conventions au niveau de l'organisation des fichiers et les
commandes de base proposées.

Notamment:

- la structure de base du système doit être décrite dans la page man
  `hier(7)`
- les commandes de la norme [*POSIX*](https://fr.wikipedia.org/wiki/POSIX)
  doivent être présentes

Linux est disponible sous forme de distributions qui, elles-mêmes, sont à
l'origine de plusieurs variantes.

Une distribution Linux est donc un assemblage de plusieurs logiciels qui
s'appuie sur le système Linux pour proposer un ensemble d'outils
cohérent.

Chaque distribution peut proposer des variations dans l'organisation des
fichiers mais elle doit toujours reporter ces variations dans la page man
`hier(7)`.

Commande permettant d'identifier la distribution utilisée: `lsb_release`

Exercice pratique:

1. Faire une recherche sur des distributions qui vous interpellent et faire
   une petite synthèse sur les intérêts que vous trouvez
2. Faites un résumé de l'arborescence de votre server privé.
3. Proposez une ligne de commande permettant d'afficher les informations de
   la distribution utilisée

## Gestion des utilisateurs

Définitions:
- compte utilisateur: ensemble d'informations qui délimite un usage
  particulier du système; pour simplifier , nous parlerons aussi
  d'utilisateur
- groupe d'utilisateurs: ensemble d'informations permettant de regrouper des
  comptes utilisateur; nous parlerons ici de *groupe*
- login: un nom permettant d'identifier un compte utilisateur
- UID: numéro permettant d'identifier un compte utilisateur
- home: le dossier d'accueil associé à un compte utilisateur
- GID: numéro permettant d'identifier un groupe d'utilisateur

Au niveau d'un système nous retrouverons 4 catégories d'actions sur les
utilisateurs et les groupes:

1. Consultation: cette catégorie regroupe toutes les commandes permettant
   de connaître les utilisateurs ou groupes qui existent dans le système
2. Création ou ajout: dans cette catégorie, nous retrouverons toutes les
   actions qui aboutissent l'existence d'un nouveau compte ou groupe dans
   le système (`useradd`, `groupadd`)
3. Modification: cette catégorie regroupe toute action qui changera les
   informations (usermod, passwd, groupmod...)
4. Suppression: toute action de cette cette catégorie aboutit à
   l'effacement du compte ou groupe du système (`userdel`, `groupdel`)

Commandes à apprendre:

- `getent`: outil de counsultation de listes d'information
    ```bash
    # getent <liste> [<id>]
    ```
- `useradd`: création d'utilisateur
    ```bash
    # useradd [<option>...] <login>
    ```
- `passwd`: attribution ou changement du mot de passe d'un utilisateur
    ```bash
    # passwd [<login>]
    ```
- `usermod`: changement des informations d'un utilisateur
    ```bash
    # usermod [<option>...] <login>
    ```
- `userdel`: suppression d'un compte utilisateur
    ~~~bash
    # userdel <login>
    ~~~
- `groupadd`: création d'un nouveau groupe
    ~~~bash
    # groupadd <groupe>
    ~~~
- `adduser`: ajout d'un utilisateur dans un groupe
    ~~~bash
    # adduser <login> <group>
    ~~~
- `deluser`: enlève un utilisateur d'un groupe
    ~~~bash
    # deluser <login> <group>
    ~~~
- `groupdel`: suppression du group
    ~~~bash
    # groupdel <group>
    ~~~

Mises en pratique:

1. Création simple d'un utilisateur `user1`:
   1. Vérifier que le compte n'existe pas en regardant l'affichage de la
      commande suivante:
      ~~~bash
      # getent passwd user1
      ~~~
   2. Exécuter la ligne de commande suivante:
      ~~~bash
      # useradd user1
      ~~~
   3. Donner une ligne de commande qui aide à savoir su l'e compte a été
      créé
   4. Le home a-t-il été créé?
   5. Effacer l'utilisateur avec la ligne de commande:
      ~~~bash
      # userdel user1
      ~~~
   6. Recréer l'utilisateur user1 avec la bonne option pour que le home
      soit créé.
2. Création complète d'un utilisateur:
   1. En lisant la page `man`de `useradd`, vous trouverez les options pour
      faire en sorte de créer automatiquement le home et spécifier le bon
      shell à attribuer à l'utilisateur.
   2. Avec les options trouvées dans la question précédente, créez
      l'utilisateur `user2`
   3. Pour que l'utilisateur puisse se connecter, il faut qu'il ait un mot
      de passe. Attribuez donc un mot de passe:
      ~~~bash
      # passwd user2
      ~~~
   4. Vérifiez que vous puissiez vous connecter au compte `user2`
3. Jeu en groupe
   1. Pour cet exercice, nous considérons que deux comptes, `user1` et
      `user2`, existent déjà dans le système. Si tetr n'est pas le cas,
      créez-les.
   2. Vérification des groupes dans lesquels se trouve user1:
      ~~~bash
      # id user1
      ~~~

      Observez le résultat et comparez la même commande avec `user2`
   3. Observez les groupes existant sur le système:
      ~~~bash
      # getent group
      ~~~
   4. Créer le groupe `tourisc`:
      ~~~bash
      # groupadd tourisc
      ~~~
   5. Vérifiez que le groupe existe bien
   6. Ajouter l'utilisateur `user1` dans le groupe `tourisc`
   7. Vérifiez que l'utilisateur soit bien dans le groupe `tourisc`:
      ~~~bash
      # getent group tourisc
      ~~~
   8. Trouvez un autre moyen de vérifier que l'utilisateur `user1` est bien
      dans le groupe `tourisc`
   9. Ajoutez le compte `user2` dans le groupe `tourisc`
   10. Vérifiez que les 2 utilisateurs soient bien dans le groupe `tourist`
4. Changez le login de `user1` en `adoy`

## Gestion de pare-feu et notions de sécurité

## Expressions rationnelles

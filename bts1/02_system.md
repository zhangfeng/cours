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

Linux est disponible sous forme de distributions qui, elles-mêmes sont à
l'origine de plusieurs variantes.

Une distribution Linux est donc un assemblage de plusieurs logiciels qui
s'appuient dur le système linux pour proposer un ensemble d'outils
cohérent.

Chaque distribution peut proposer des variations dans l'organisation des
fichiers mais elle doit toujours reporter ces variations dans la page man
`hier(7)`.

Commande permettant d'identifier la distribution utilisée: `lsb_release`

Exercice pratique:

1. Faire une recherche sur des distributions qui vous interpellent et faire
   une petite synthèse sur les intérêts que vous trouvez
2. Faites un résumé de l'arborescence de votre server privé.

## Gestion des utilisateurs

Définitions:
- compte utilisateur: ensemble d'informations qui délimite un usage
  particulier du système
- groupe d'utilisateur: ensemble d'informations permettant de regrouper des
  comptes utilisateur
- login: un nom permettant d'identifier un compte utilisateur
- UID: numéro permettant d'identifier un compte utilisateur
- home: le dossier d'accueil associé à un compte utilisateur
- GID: numéro permettant d'identifier un groupe d'utilisateur

## Gestion de pare-feu et notions de sécurité

## Expressions rationnelles

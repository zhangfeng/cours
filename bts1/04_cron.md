---
title: Plannification de tâches sous Linux
layout: folder
---

## Introduction

Sur un ordinateur, nous avons besoin d'effectuer des tâches régulière.

Malheureusement, la vie fait que nous pouvons facilement oublier car nous
sommes pris sur d'autres tâches.

Ayant conscience de cet état de fait, les créateurs d'`Unix` ont pensé un
système de plannification basé sur des déclarations de commandes que nous
voulons exécuter périodiquement: `cron`.

## La commande de plannification `crontab`

Sous `Unix`, chaque compte utilisateur a son propre plannificateur de
tâche.

Il se gère via la commande `crontab`.

Pratique: lister les lignes de commande plannifiées:
   ```bash
   # crontab -l
   ```

Lisez ce qu'affiche la ligne de commande

Pour plannifier des tâches, nous devons utiliser l'option `-e`.

Tapez La ligne de commande:
```bash
# crontab -e
```

Sous `Debian`, la première fois que vous lan'ez cette ligne de commande, il
vous demandera de cgoisir un éditeur.

Analysez les commentaires du fichier qui s'ouvre.

La syntaxe qui s'en dégage:
- une déclaration est une ligne qui se compose de 6 champ:

  1. la minute à laquelle devra se lancer la ligne
  2. l'heure du lancement
  3. le jour dans le mois du lancement
  4. le numéro du mois
  5. le jour dans la semaine du lancement (1 = lundi)
  6. la ligne de commande

Dès que vous sauvegardez, le plannificateur sera mis à jour.

Exercice: plannifiez le lancement de la ligne de commande "`date >> bonjour`"

Vérifiez que la commande s'est biem exécutée.

## Périodicité des exécutions

Chaque champ précisant la date peut avoir plusieurs forme:

- un nombre:
  - 0-59 pour les champs minute et heure,
  - 1-31 pour les jour du mois,
  - 1-12 pour les mois,
  - 0-7 pour les jours de semaine
- deux nombres séparés par un tiret `-` pour inclure toutes les valeurs
  entre les deux (inclusif)
- une astérisque `*` suivie d'un `/` et d'un diviseur: cela indique que sont retenues
  toutes les valeurs multiples du diviseur
- une liste composée de toutes les formes précédentes séparées par des
  virgules `,`
- une astérisque `*` pour indiquer TOUTE les valeurs

Questions:

1. si l'on met */3 dans les minutes, est-ce que la tâche s'exécutera toutes
   les 3 minutes?
2. même question pour 7?

## Pour aller plus loin

Pour aller plus loin, vous pouvez consulter les pages `man` de `crontab` et
`cron`.

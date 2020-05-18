---
title: Expressions rationnelles ou régulières
layout: folder
---

## Concepts

Les expressions rationnelles ou régulières permettenet de reconnaître des
mots ou textes qui respectent un motif.

Un motif est un ensemble de caractères définissant à quoi ressemblent les
textes souhaités.

Un motif peut être composé de motifs et d'atome.

Un atome est un motif non décomposable.

Dans le domaine des expressions rationnelles, les atomes sont:
- les caractères imprimables exceptés `+`, `?`, `*`, `|`, `[`, `]`,
  `{`, `}`, `(`, `)`, et ` `
- tout motif entouré de `(` et `)`
- une suite de caractères entourés de `[` et `]`

L'ensemble de mots reconnus par une expression rationnelle est son langage.

## Première mise en pratique

Dans le monde `Unix`, les outils de reporting et de recherche de texte
s'appuient beaucoup sur les expressions rationnelles.

1. Recherche de ligne avec `egrep` (ou `grep -E`)
   
   Exécuter la ligne de commande suivante:

   ```bash
   $ getent passwd \ egrep root
   ```

2. Un caractère pour tous

   Dans les caractères imprimables, certains ont une signification
   spéciale. `.` permet de reconnaître n'importe quel caractère.

   Exécuter:

   ```bash
   # egrep '14:..:..' /var/log/syslog
   ```

   Chercher une ligne de commande permettant d'afficher tout les événements
   de 11:00 à 11:59

3. Le début et fin de ligne

   Parmi les caractères séciaux, nous avons `^` qui permet de représenter
   le début de ligne s'il est au début de l'eyperssion et `$` représente la
   fin de ligne.

   Exécuter:

   ```bash
   # egrep ^r..t /etc/passwd
   ```

   Puis:

   ```bash
   # egrep 'sh$' /etc/passwd
   ```

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

Dans une expression rationnelle, tout atome peut être "quantifié" ce qui
signifie que, dans les mots reconnus, l'atome peut apparaître un certain
nombre fois selon le quantifieur. Les quantifieurs possibles sont:

- `?` l'atome précédent peut apparaître 0 ou 1 fois dans les mots reconnus
- `+` l'atome précédent doit apparaître au minimum une fois (pas de
  maximum)
- `*` l'atome précédent peut apparaître 0, 1 ou plusieurs fois.
- `{n,m}` l'atome précédent doit apparaître au moins `n` fois et au maximum  `m` fois. `n` et `m` sont facultatif et, s'ils sont omis sont remplacé par:

  - `n` par 0
  - `m` par l'infini

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

4. Les classes de caractères

   Exécuter:

   ```bash
   # egrep '1[123]:..:' /var/log/syslog
   ```

   Ici, à l'intérieur des `[` et `]`, les caractères consécuvifs peuvent
   exprimés sous la forme `[1-9]`.

   En vous inspirant de l'exemple précédent, faire afficher les lignes du
   `syslog` qui correspondent de 10:00 à 14:59

5. En utilisant `awk`, faites afficher le nom des processus qui ont généré
   des événements entre 11:00 et 12:59 ainsi que l'horaire des événements.

## Références

Lire les `man` de `grep et `awk`, en particulier les sections décrivant les
expressions rationnelles (Regular Expressions)

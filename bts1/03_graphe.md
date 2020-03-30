---
title: Représentation de schémas et collaboration
layout: folder
---

## Objectif

Les schémas permettent d'appréhender des concepts basés sur des
cheminements d'idées.

La problématique que nous allons traiter ici est: comment faire en sorte
que les schémas puissent être compris par des personnes ne pouvant pas
acquérir une représentation visuelle.

## Une solution

Une des pistes possibles est la description détaillée du schéma.

L'outil [graphviz](https://graphviz.gitlab.io/) propose une solution basée
sur un langage simple, `dot`.

Dans ce langage, nous partons du principe qu'un schéma (ou `graph`   dans le
langage `dot`) est constitué essentiellement de deux types
d'élément:

1. les noeuds: ils permettent de représemter des entités, des états, des
   objets... En `dot`, ce sont juste des noms (entre guillemets s'ils
   contiennent des espaces)
2. des fils: ils permettent de représenter des relations ou cheminements
   entre les noeuds. Ils sont représentés en `dot` par la suite de
   caractères `->` pour un fil orienté ou `--` pour un fil non-orienté.

Tous ces éléments possèdent plusieurs attributs modifiables (voir les
exemples plus loin).

## Exemples

Ici quelques exemples. Pour alléger la page, seules les images sont
visibles. Pour avoir la description `graphviz`, cliquez sur l'image.

[![Circulation de la saisie]({% link assets/saisie.png %})]({% link assets/saisie.gv %})

[![Système de mail]({% link assets/mail.png %})]({% link assets/mail.gv %})

[![Réseau domestique]({% link assets/reseau.png %})]({% link assets/reseau.gv %})

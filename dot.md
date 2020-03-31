---
title: DOT ou un moyen de créer des schémas en texte uniquement
layout: standalone
permalink: /dot
---

## Les schémas

Les schémas permettent aux personnes qui peuvent voir une image
d'appréhender de nouveaux concepts. Effectivement, ils permettent de
représenter visuellement une cheminement de penser. Que se passent-ils
lorsque vous demandez à une personne qui vient de voir un schéma de
formaliser ce qu'il a compris?

Tout d'abord, elle essaiera de décrire le schéma avec ces propres mots puis
précisera ce qu'il en a déduit (son interprétation).

## Description et collaboration

Pour qu'un aveugle ou un mal-voyant qui ne peut voir les images puisse
comprendre les schémas, il faut réussir à les décrire de manière
systématique (qui suit un système) et simple.

Si l'on analyse un schéma, il est composé de 4 types d'informations:

- des entités: des petites icônes représentant des objets, des états, des
  étapes...
- des relations: des lignes qui relient les entités pouvant représenter des
  évolutions, des chemins ou des liens
- des étiquettes: textes courts permettant de nommer les entités et/ou les
  relations
- des informations visuelles: des éléments permettant de suggérer des
  différences eftre les entités et/ou les relations; exemples d'information
  visuelle: la couleur des entités, la forme des entités, le style des
  relations.

## Une solution

Le logiciel [`graphviz`](https://www.graphviz.org) propose des outils en
ligne de commande permettant de manipuler des fichiers contenant des
descriptions textuelles de schéma (graphe dans leur jargon). Ce langage
contient tout ce qu'il faut pour représenter les 4 types d'information
cités dans le paragraphe précédent.

Voici un résumé non exhaustif de ce langage simple:

- les entités sont représentés par dis noms que le créateur du fichier va
  fixer
- les relations sont représentées de deux manières:
  - entite1 `--` entite2: une relation simple, matérialisée par
    une ligne
  - entite1 -> entite2: relation orientée, matéralisée par une flèche dont
    la pointe est dirigée vers entite2
- les étiquettes sont associées, via un système d'attributs, aux différents
  éléments (entités ou relations);
- les autres informations visuelles sont associées aux relations et entités
  via le système d'attributs.
- les attributs se déclarent entre crochets (`[` et `]`) après les éléments
  concernés sous la forme `attribut=valeur`

La ligne de commande permettant de générer une image à partir du fichier
contenant le langage est

```
# dot -Tpng fichier.gv -o image.png
```

Dans la ligne de commande modèle,:

- `fichier.gv` contient le langage de description de schéma (le `DOT`)
- `-Tpng` indique la génération d'une image au format `PNG` (les peuvenct
  être aussi `-Tjpg` pour du `JPEG` ou encore `-Tpdf` pour du `PDF`)
- `image.png` est le nom du fichier image généré.

## Installation de `graphviz`

Sous `Linux`, `graphviz` est inclus dans les dépôts traditionnels donc il
s'install sans difficulté:

- Sous `Debian` et `Ubuntu`:
  ```bash
  # apt-get install graphviz
  ```
- Sous `CentOS`:
  ```bash
  # yum install graphviz
  ```
- Sous `Fedora`:
  ```bash
  # dnf install graphviz
  ```

Sous `Windows`, il faut réaliser 3 étapes:

1. Télécharger l'anstallation de `graphviz` sur
   https://graphviz.gitlab.io/_pages/Download/windows/graphviz-2.38.msi
2. Installer `graphviz` en notant bien le dossier dans lequel il sera
   installé
3. Ajouter le sous-dossier `\bin` de l'installation dans la variable
   d'environnement `PATH` de votre utilisateur

## Exemples

Ici, vous trouverez des exemples de schémas que j'ai réalisés. Pour
afficher le fichier source, il suffit de cliquer sur l'image
correspondante.

[![Circulation de l'information lors de la saisie]([% link assets/saisie.png %])]([% link assets/saisie.gv %])

[![Circuit d'un mail]([% link assets/mail.png %])]([% link assets/mail.gv %])

[![un réseau domestique]([% link assets/reseau.png %])]([% link assets/reseau.gv %])

Remarques:

- Dans les deux premières représentations, un graphe orienté est utilisé
  pour bien insister sur le sens de circulation de l'information. Remarquez
  l'utilisation du mot-clé `digraph` en début de fichier
- Le troisième schéma n'est pas orienté, c'est-à-dire que les relations ne
  représentent qu'un lien (par exemple un câble). Remarquez la présence du
  mot-clé `graph` en début de fichier
- pour généré les schémas, la ligne de commande citée élus a été utilisée.

## Exercices pour pratiquer

Pour apprendre et pratiquer, je vous propose de faire quelques-uns de ces
exercices:

1. Créer un schéma représentant votre propre réseau domestique
2. Créer un schéma représentant votre domicile. Ici, ne cherchez pas à
   représenter le plan de votre maison mais surtout les pièces et comment
   elles sont reliées entre elles.
3. Imaginez que vous organisiez un circuit touristique et réalisez un
   schéma qui montre les différentes étapes de votre circuit.

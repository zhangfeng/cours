---
title: Outils d'aide au reporting
layout: folder
---

## Concepts

Les services s'appuient sur des programmes qui tournent en permanence.
Comme ces programmes s'exécute en arrière-plan, ils ne sont donc rattachés
à aucun affichage. Pour répondre à cette problématique, toutes
communication d'information de ces programmes passe par des fichiers de
trace: journaux (logs dans le jargon).

Les journaux ou logs sont donc des fichiers textes pouvant contenir tout
type d'information affichable.

Le défi de l'administrateur est donc de pouvoir comprendre ces informations
et d'en extraire les plus significatives pour analyser un fonctionnement ou
un dysfonctionnement.

Enfin, à partir des informations considérées importantes, il doit créer des
rapports lisibles.

Rapport: assemblage d'informations permettant de répondre à une question ou
une problématique.

Le secret de l'administrateur: maîtriser les outils adaptés pour extraire
les informations et les présenter de manière lisible.

## Outils mis à disposition

Les plus simples, affichage pur:

- cat
- less
- compresseurs (gzip, bzip2...)

Un peut plus avancés, permettent de découpé l'information:

- head
- tail
- cut
- sort
- grep

Avancés, ces outils su suffisent à eux-mêmes:

- sed
- awk
- perl
- python

## Pratique

1. Exécuter la commande suivante:
   
   ```bash
   # cat /var/log/syslog
   ```

   Décrivez l'affichage que vous voyez et mettez par écrit vos constats.

2. Exécuter la commande:
   
   ```bash
   # less /var/log/syslog
   ```

   Notez la différence avec l'étape précédente et tapez `q` lorsque vous
   avez fini de regarder.

3. Pour cette étape, notez que la commande `nl` permet de numéroter les
   ligne. Exécuter la commande suivante:

   ```bash
   # head /var/log/syslog
   ```

   Pour mieux comprendre l'affichage, exécuter:

   ```bash
   # nl /var/log/syslog | head
   ```

   Que constatez-vous? Pouvez-vous dire à quoi correspond ce que vous
   voyez?

4. Exécuter:

   ```bash
   # tail /var/log/syslog
   ```

   Comment interprétez-vous ce que vous voyez?

   Continuez avec la commande:

   ```bash
   # nl /var/log/syslog | tail
   ```

   Notez vos conclusions.

5. Notion de filtrage
   
   Pour chacune des étapes ci-dessous, notez vos impressions, constats et conclusions

   1. Exécuter:

      ```bash
      # nl /var/log/syslog
      ```

      Puis:

      ```bash
      # cat /var/log/syslog | nl
      ```

   2. Exécuter:

      ```bash
      # nl /var/log/syslog | head
      ```

      Puis:

      ```bash
      # head /var/log/syslog | nl
      ```

   3. Exécuter:

      ```bash
      # nl /var/log/syslog | head -15
      ```

      Puis:

      ```bash
      # nl /var/log/syslog | tail -15
      ```

6. Extraction

   Le but des exercices suivants est de simplifier l'effort de lecture pour
   l'administrateur. Pour chaque étape, notez vos constats et conclusions.

   1. Sélection de ligne par les numéros:

      Exécuter:

      ```bash
      # nl /var/log/syslog | head -15 | tail
      ```

      Comment afficher les lignes 21 à 23?

   2. Sélection de lignes

      Exécuter:
   
      ```bash
      # grep 09: /var/log/syslog
      ```
   
      Puis:
   
      ```bash
      # grep ' 09:' /var/log/syslog
      ```
   
      Comment faire en sorte qu'on voie que les lignes entre 11:00 et 12:00?

   3. Extraction de colonnes

      Exécuter:

      ```bash
      # getent passwd | cut -d: -f1
      ```

      Puis:

      ```bash
      # getent passwd | cut -d: -f1,5
      ```

      Comment faire en sorte que le `:` ne soit pas afficher (lecture de
      `man`)?

   4. Exécuter:

      ```bash
      # grep ' 09:' /var/log/syslog | cut -f1
      ```

      Notez vos commentaires et expliquez la sortie.

      Comment peut-on faire en sorte que `cut` affiche les colonnes que
      l'on veut dans ce cas?

   5. Exécuter:

      ```bash
      # awk '{ print $3 }' /var/log/syslog
      ```

      Interpréter la sortie.

      Puis:

      ```bash
      # awk '{ print $1,$2,$3 }' /var/log/syslog
      ```

      Puis:

      ```bash
      # awk '{ print "Exécution:", $1,$2,$3 }' /var/log/syslog
      ```

   6. Exécuter:

      ```bash
      # awk '/ 09:/ { print "Date:", $1,$2,$3, "Programme:", $5 }' /var/log/syslog
      ```

7. Réaliser le programme `head` simplifié avec `awk`

8. Réaliser le programme `nl` simplifié avec `awk`

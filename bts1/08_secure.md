---
title: Les bases de la sécurité des serveurs
layout: folder
---

## Concepts et mots clés

Sécurité:
- firewall, Internet, ports, protection, sauvegarde,
- sécurité physique
- sauvegarde des données
- surveillance,
- sécurité.

Outils connus:
- iptables, fail2ban
- pare-feu
- antivirus
- sauvegarde

Définition de sauvegarde: un stockage des données à un temps précis dans le
but de secours.

Archivage: stockage de données longue durée à des fins potentielles de
relecture.

## Les différents domaines de base de la sécurité

La sécurité numérique inclus plusieurs domaines pour les mêmes objectifs: s'assurer
de l'authenticité des données et la protection contre la reproduction et la
falsification.

Généralement, on inclut les domaines suivants:
- l'authentification: les actions et ressources permettant d'être sûr que
  l'interlocuteur est celui qu'il prétend,
- la cryptologie: l'étude du chiffrement des données
- la gestion des accès: les différents dispositifs permettant d'exposer les
  données uniquement à leur destinatiare
- la détection et le contrôle des intrusions.
- l'ensemble des stratégies favorisant les points précédents.

## En pratique sous Linux

### Fonctionnement du pare-feu intégré au noyau Linux

Tapez:

  ~~~bash
  # iptables -L
  ~~~

Cette commande affiche l'état des chaînes actives.

Dans `iptables`, les chaînes correspondent aux chemins que suivent les
données.

Ces chemins sont constitués de règles qui permettent au noyau `Linux` de
décider quoi faire avec ces données. Les règles disposent de méta-données
comme critères.

Les chaînes de base sont:
- INPUT: le chemin des données qui viennent de l'extérieur
- OUTPUT: le chemin des données qui vont vers l'extérieur
- FORWARD: le chemin des données destinées à "traverser" l'ordinateur
  (utile si l'ordinateur en question a le rôle de passerelle)

Une règle est composée de:

1. des vérifications par rapport aux méta-données des données qui
   traversent la chaîne pour savoir si ces données sont concernées
2. une cible indiquant vers où les données concernées par la règle doivent être orientées.

Les cibles existantes par défaut sont:

- DROP: la donnée concernée est oubliée
- ACCEPT: la donnée continue son cheminement
- REJECT: la donnée est refusée et on informe l'expéditeur si besoin
- RETURN: la donnée est renvoyée à la chaîne et c'est la cible de
  l'appelant qui sera choisie.

`iptables` est l'outil qui va permettre non seulement de voir l'état et les
règles du pare-feu intégré mais également d'ajouter et de supprimer des
règles.

### Cas pratique

Pour ce cas, vous devez avoir un serveur à disposition en plus de votre
poste de travail. Pour commodité, nous appellerons le server `srv`.

1. Test d'envoi de donnée simple
   
   Dans une invite de commande de votre poste de travail, tapez:

   ```
   $ ping srv
   ```

   Vous avez en principe une réponse indiquant que des paquets de données
   ont été envoyés et revenus avec succès.

2. Ajout d'une règle dans la chaîne INPUT refusant des paquets

   Sur `srv` tapez et comprenez les lignes suivantes:

   ```bash
   $ iptables -A INPUT -p icmp -j REJECT
   ```

   Pour voir le résultat:

   ```bash
   $ iptables -L
   ```

3. Faire la même commande qu'au point 1 et vérifiez la sortie
4. Effacement des règles?

   ```bash
   # iptables -F INPUS
   ```
5. Une autre cible

   Refaites la commande de 2. en remplaçant `-j REJECT` par `-j DROP`

6. Refaites la commande de 1. et observez la différence


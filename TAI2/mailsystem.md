---
title: Le système de mail
layout: folder
---

Le système de mail est composé de plusieurs services:

- le service d'emvoi qui utilise le protocole `SMTP` sur le port 25,
- le service de transport qui est, dans la plupart des cas, exécuté par le
  même serveur que l'envoi; il passe par le protoôle `SMTP` également mais
  peut passer par différents ports selon la politique de l'organisme,
- enfin le service de livraison qui peut utiliser différents protoôles tels
  que POP3 ou IMAP.

Dans ce cours, nous allons essayer de mettre en place un système basique de
mail.

Pour notre cas, le but sera que vous puissiez échanger des mails via vos
VPS (serveur privé virtuel).

Pour ce faire, vous allez suivre ces étapes à votre rythme.

Pendant tous les exercices suivants, je considèrerai que vous êtes
connectés sur votre serveur.

## Packages et installation éventuelle



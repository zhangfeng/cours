---
title: Connection à un Wifi avec nmcli sous Linux
layout: folder
---

1. Lister la liste des réseaux disponibles:
   ```bash
   # nmcli d w list
   ```

   Le résultat est un tableau listant tous les réseaux à portée. Il faut
   bien repérer les noms avec leur orthographe et casse précises dans la colonne de gauche.
2. Connexion au réseau choisi (je l'appel "`Wifi Prive`" ici) avec son mot
   de passe (ici `PhrasePasse`):
   ```bash
   # nmcli d w connect 'Wifi Prive' password 'PhrasePasse'
   ```
3. Vérifiez avec n'importe quelle commande qui accède au réseau

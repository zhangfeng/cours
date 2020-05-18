---
title: Installation de Redmine sur un serveur Debian
layout: folder
---

## Objectif

À la fin de cette procédure, nous obtiendrons sur le server:

- Nginx (serveur web) installb
- Passenger (serveur d'application Ruby) installé
- Redmine (application de suivi de projets et de tickets) installé,
- MariaDB (serveur de base de données) installé
- un gestion autonome de certificat SSL via Certbot

## Pré-requis

Dans cette procédure, nous partons d'une Debian 10 (Buster) fraîchement
installé.

Durant toute la procédure, nous considérons que nous sommes connecté en
tant que `root`.

## Procédure

1. Mis à jour des dépôts et packages installés:

   ```bash
   # apt update && apt -y full-upgrade
   ```

2. Redémarrage du système au cas où le noyau a été mis à jour:
   
   ```bash
   # systemctl reboot
   ```

   Se reconnecter en tant que `root` pour la suite.

3. Installation des dépendances:

   ```bash
   # apt install mariadb-server mariadb-client libmariadbclient-dev imagemagick libmagickwand-dev libcurl4-openssl-dev git-core subversion gpg curl
   ```

4. Installation de Ruby 2.6 et de RVM (permet de gérer plusieurs versions
   de Ruby

   Importation de clés de vérification:

   ```bash
   # gpg --keyserver hkp://pool.sks-keyservers.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
   ```

   Installation de Ruby 2.6:

   ```bash
   # curl -L https://get.rvm.io | bash -s stable --ruby=2.6
   ```

   Ajout de l'initialisation de l'environnement `rvm` à l'ouverture du
   shell:

   ```bash
   # echo '[[ -s "/usr/local/rvm/scripts/rvm" ]] && source "/usr/local/rvm/scripts/rvm"' >> ~/.bashrc
   ```

   Initialisation de l'environnement `rvm` pour la session courante:

   ```bash
   # source "/usr/local/rvm/scripts/rvm"
   ```

5. Configuration de `MariaDB` pour `redmine`
   
   Se connecter à la base en tant que root (pour l'instant, pas de mot de
   passe pour le compte `root` car fraîchement installé):

   ```bash
   # mysql
   ```

   Puis création de base et d'utilisateur pour `redmine`:

   ```sql
   MariaDB []> create database redmine;
   MariaDB []> grant all privileges on redmine.* to redmine@localhost identified by 'rEdMiNe_p@ss0rd';
   MariaDB []> flush privileges;
   MariaDB []> quit;
   ```

   Pour des raisons de sécurité, changez le mot de passe

6. Install de `passenger` (serveur d'application) et `nginx` (serveur Web):

   Installation de `passenger` avec le module d'intégration à `nginx`:

   ```bash
   # gem install passenger -- --no-ri --no-rdoc
   # passefger-install-nginx-module
   ```

   Voici les réponses pour les étapes de `passenger-install-nginx-module`:

   - Taper `entrée` sur l'information
   - tapez `!` pour que le menu se présente correctement pour l'interface
     texte
   - taper juste `entrée` pour valider les choix de langages par défaut
     (Ruby et Python)
   - taper `1` pour choisir l'installation et compilation de `nginx`
   - Taper `entrée` pour accepter le choix par défaut de dossier où
     installer `nginx`,
   - taper `entrée` pour accepter le message d'information.

7. Configuration de `nginx`

   Dans le dossier de configuration de `nginx`, Editer `nginx.conf`i pour
   ajouter une ligne pour gérer le dossier `vhosts`:

   ```bash
   # cd /opt/nginx/conf
   # sed -i -e '$i include vhosts/*.conf;' nginx.conf
   ```

   Maintenant, il faut créer le dossier qui recevra les configuratins des
   vhosts:

   ```bash
   # mkdir /opt/nginx/conf/vhosts
   ```

   Édition du fichier `/opt/nginx/conf/vhosts/redmine.conf` en y collant le
   contenu suivant:

   ```
   server {
       listen 80;
       server_name nom.server.com;
       root /var/www/redmine/public;
       passenger_enabled on;
       client_max_body_size 10m;
       error_page 500 502 503 504 /50x.html;
       location = /50x.html {
         root html;
       }
   }
   ```

   Ajout d'un fichier pour que `nginx` se lance au démarrage de `systemd`:

   Créer un fichier /opt/

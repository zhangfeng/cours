---
title: Installation de GLPI sur un serveur Debian Buster
layout: folder
---

## Objectif

Installation de GLPI sur un LAMP

## Procédure

1. Mise à jour du système en `root`:

   ~~~bash
   # apt-get update && apt-get full-upgrade && systemctl reboot
   ~~~

2. Installation d'Apache et de PHP

   ~~~bash
   # apt-get install php7.3 php-{pear,gettext,cas,apcu} php7.3-{curl,zip,gd,intl,imagick,imap,memcache,pspell,recode,tidy,xmlrpc,xsl,mbstring,ldap,mysql} libapache2-mod-php7.3
   ~~~

3. Installation de MariaDB (serveur de bases de données)

   ~~~bash
   # apt-get install mariadb-{client,server}
   ~~~

4. Configuration de base de données

   Dans le terminal, entrer dans le client `MariaDB` en entrant la ligne
   suivante:

   ~~~bash
   # mysql
   ~~~

   Les commandes suivantes seront à lancer dans le client comme indiqub par
   l'invite.

   Création de la base de données pour `GLPI`:

   ~~~
   MariaDB [(none)]> CREATE DATABASE glpidb;
   ~~~

   Création de l'utilisateur `glpiuser` et attribution d'accès à la base:

   ~~~
   MariaDB [(none)]> grant all privileges on glpidb.* to glpiuser@localhost identified by 'SuperMotDePasse';
   ~~~

   Vous pouvez vérifier que tout a été créé correctement avec la commande
   suivante:

   ~~~
   MariaDB [(none)]> select User,Host,Db from mysql.db;
   ~~~

   Si tout s'est bien passé, la commande précédente affiche une ligne de la
   base contenant l'utilisateur et la base créés.

   Enfin, pour sortir du client, entrer la commande `exit;` ou le raccourci
   clavier `CTRL-D`.

5. Téléchargement et installation de `GLPI 9.4.3`

   ~~~bash
   # wget -O- https://github.com/glpi-project/glpi/releases/download/9.4.3/glpi-9.4.3.tgz | tar xzfC - /var/www/html && cd /var/www/html && chown -R www-data:www-data . && chmod -R 755 .
   ~~~
   
   Si tout s'est bien passé, nous nous retrouvons dans le dossier
   `/var/www/rtml`

6. Création d'un hôte virtuel pour `Apache` (le serveur web)

   Pour cela, créez le fichier `/etc/apache2/sites-available/glpi.conf` et
   collez le contenu suivant dedans:

   ~~~
   <VirtualHost *:80>
      ServerAdmin admin@your_domain.com
      DocumentRoot /var/www/html/glpi
      ServerName your-domain.com 
      <Directory /var/www/html/glpi>
         Options FollowSymlinks
         AllowOverride All 
         Require all granted
      </Directory>
      ErrorLog ${APACHE_LOG_DIR}/your-domain.com_error.log
      CustomLog ${APACHE_LOG_DIR}/your-domain.com_access.log combined
   </VirtualHost>
   ~~~

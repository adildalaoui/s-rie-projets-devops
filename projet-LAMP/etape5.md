# STEP 5 — ACTIVER PHP SUR LE SITE WEB

Avec les paramètres par défaut de DirectoryIndex sur Apache, un fichier nommé index.html prendra toujours la priorité sur un fichier index.php. Cela est utile pour mettre en place des pages de maintenance dans des applications PHP, en créant un fichier temporaire index.html contenant un message informatif pour les visiteurs. Comme cette page aura priorité sur la page index.php, elle deviendra la page d'accueil de l'application. Une fois la maintenance terminée, le fichier index.html est renommé ou supprimé du répertoire de documents, et la page normale de l'application réapparaîtra.

Si vous souhaitez changer ce comportement, vous devrez modifier le fichier /etc/apache2/mods-enabled/dir.conf et changer l'ordre dans lequel le fichier index.php est listé dans la directive DirectoryIndex :

```
sudo vim /etc/apache2/mods-enabled/dir.conf
```

```
<IfModule mod_dir.c>
        #Change this:
        #DirectoryIndex index.html index.cgi index.pl index.php index.xhtml index.htm
        #To this:
        DirectoryIndex index.php index.html index.cgi index.pl index.xhtml index.htm
</IfModule>
```

Après avoir sauvegardé et fermé le fichier, vous devrez recharger Apache pour que les modifications prennent effet :

```
sudo systemctl reload apache2
```

Enfin, nous allons créer un script PHP pour vérifier que PHP est correctement installé et configuré sur votre serveur.

Maintenant que vous avez un emplacement personnalisé pour héberger les fichiers et dossiers de votre site web, nous allons créer un script de test PHP pour confirmer qu'Apache est capable de traiter les requêtes des fichiers PHP.

Créez un nouveau fichier nommé index.php dans votre répertoire web personnalisé :
```
vim /var/www/projectlamp/index.php
```

Cela ouvrira un fichier vierge. Ajoutez le texte suivant, qui est un code PHP valide, à l'intérieur du fichier :
```
<?php
phpinfo();
```

Une fois terminé, sauvegardez et fermez le fichier. Rafraîchissez la page dans votre navigateur, et vous verrez une page similaire à celle-ci :

![projject1-step5](https://user-images.githubusercontent.com/85270361/210115357-dfca0250-7e0b-4f3c-8e26-8266be9cc4a6.PNG)


Cette page fournit des informations sur votre serveur du point de vue de PHP. Elle est utile pour le débogage et pour s'assurer que vos paramètres sont correctement appliqués.

Si vous pouvez voir cette page dans votre navigateur, cela signifie que l'installation de PHP fonctionne comme prévu.

Après avoir vérifié les informations pertinentes sur votre serveur PHP via cette page, il est préférable de supprimer le fichier que vous avez créé, car il contient des informations sensibles sur votre environnement PHP et votre serveur Ubuntu. Vous pouvez utiliser rm pour le faire :

```
sudo rm /var/www/projectlamp/index.php
```

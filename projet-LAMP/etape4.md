# STEP 4 — CRÉATION D'UN HÔTE VIRTUEL POUR VOTRE SITE WEB AVEC APACHE

Dans ce projet, vous allez configurer un domaine appelé projectlamp, mais vous pouvez le remplacer par n'importe quel domaine de votre choix.

Apache sur Ubuntu 20.04 dispose d'un bloc de serveur activé par défaut qui est configuré pour servir des documents depuis le répertoire /var/www/html. Nous allons laisser cette configuration telle quelle et ajouter notre propre répertoire à côté du répertoire par défaut.

Créez le répertoire pour projectlamp en utilisant la commande mkdir comme suit :
```
sudo mkdir /var/www/projectlamp
```

Ensuite, attribuez la propriété du répertoire à votre utilisateur système actuel :

```
sudo chown -R $USER:$USER /var/www/projectlamp
```

Puis, créez et ouvrez un nouveau fichier de configuration dans le répertoire sites-available d'Apache en utilisant votre éditeur de ligne de commande préféré. Ici, nous allons utiliser vi ou vim (ce sont les mêmes d'ailleurs) :

```
sudo vi /etc/apache2/sites-available/projectlamp.conf
```

Cela va créer un nouveau fichier vide. Collez la configuration minimale suivante en appuyant sur i sur le clavier pour entrer en mode insertion, puis collez le texte :

```
<VirtualHost *:80>
    ServerName projectlamp
    ServerAlias www.projectlamp 
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/projectlamp
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
```

Pour sauvegarder et fermer le fichier, suivez simplement les étapes ci-dessous :

Appuyez sur la touche esc du clavier
Tapez :
Tapez wq (w pour write et q pour quit)
Appuyez sur ENTRÉE pour sauvegarder le fichier
Vous pouvez utiliser la commande ls pour afficher le nouveau fichier dans le répertoire sites-available :

```
sudo ls /etc/apache2/sites-available
```

Vous verrez quelque chose comme ceci :
```
000-default.conf  default-ssl.conf  projectlamp.conf
```

Avec cette configuration de VirtualHost, nous indiquons à Apache de servir projectlamp en utilisant /var/www/projectlamp comme répertoire racine web. Si vous souhaitez tester Apache sans nom de domaine, vous pouvez supprimer ou commenter les options ServerName et ServerAlias en ajoutant un caractère # au début des lignes correspondantes. L'ajout de ce caractère indiquera au programme d'ignorer ces instructions.

Vous pouvez maintenant utiliser la commande a2ensite pour activer le nouvel hôte virtuel :

```
sudo a2ensite projectlamp
```

Il est possible que vous souhaitiez désactiver le site par défaut installé avec Apache. Cela est nécessaire si vous n'utilisez pas de nom de domaine personnalisé, car dans ce cas, la configuration par défaut d'Apache écraserait votre hôte virtuel. Pour désactiver le site par défaut d'Apache, utilisez la commande a2dissite en tapant :
```
sudo a2dissite 000-default
```

Pour vous assurer que votre fichier de configuration ne contient pas d'erreurs de syntaxe, exécutez :
```
sudo apache2ctl configtest
```

Enfin, rechargez Apache pour que ces modifications prennent effet :

```
sudo systemctl reload apache2
```

Votre nouveau site est maintenant actif, mais le répertoire web /var/www/projectlamp est encore vide. Créez un fichier index.html à cet emplacement pour tester si l'hôte virtuel fonctionne comme prévu



Allez maintenant sur votre navigateur et essayez d'ouvrir l'URL de votre site en utilisant l'adresse IP publique :

```
http://<Public-IP-Address>:80
```

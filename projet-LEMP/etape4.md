# STEP 4 — CONFIGURATION DE NGINX POUR UTILISER LE TRAITEMENT PHP

Lors de l'utilisation du serveur web Nginx, nous pouvons créer des blocs de serveur (similaires aux hôtes virtuels dans Apache) pour encapsuler les détails de configuration et héberger plusieurs domaines sur un seul serveur. Dans ce guide, nous utiliserons projectLEMP comme exemple de nom de domaine.

Sur Ubuntu 20.04, Nginx a un bloc de serveur activé par défaut et est configuré pour servir des documents à partir d'un répertoire situé à /var/www/html. Bien que cela fonctionne bien pour un site unique, cela peut devenir difficile à gérer si vous hébergez plusieurs sites. Au lieu de modifier /var/www/html, nous allons créer une structure de répertoire dans /var/www pour le site your_domain, laissant /var/www/html en place comme répertoire par défaut à servir si une requête client ne correspond à aucun autre site.

Créez le répertoire racine du web pour your_domain comme suit :
```
sudo mkdir /var/www/projectLEMP
```

Ensuite, attribuez la propriété du répertoire à la variable d'environnement $USER, qui fera référence à votre utilisateur système actuel :

```
sudo chown -R $USER:$USER /var/www/projectLEMP
```

Puis, ouvrez un nouveau fichier de configuration dans le répertoire sites-available de Nginx en utilisant votre éditeur de ligne de commande préféré. Ici, nous allons utiliser nano :

```
sudo nano /etc/nginx/sites-available/projectLEMP
```

Cela créera un nouveau fichier vide. Collez-y la configuration de base suivante :

```
#/etc/nginx/sites-available/projectLEMP

server {
    listen 80;
    server_name projectLEMP www.projectLEMP;
    root /var/www/projectLEMP;

    index index.html index.htm index.php;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
     }

    location ~ /\.ht {
        deny all;
    }

}
```

Voici ce que chaque directive et bloc de localisation fait :

listen — Définit le port sur lequel Nginx écoutera. Dans ce cas, il écoutera sur le port 80, le port par défaut pour HTTP.
root — Définit le répertoire racine où les fichiers servis par ce site sont stockés.
index — Définit dans quel ordre Nginx donnera la priorité aux fichiers index pour ce site. Il est courant de lister les fichiers index.html avec une priorité plus élevée que les fichiers index.php pour permettre la mise en place rapide d'une page de maintenance dans les applications PHP. Vous pouvez ajuster ces paramètres pour mieux répondre aux besoins de votre application.
server_name — Définit quels noms de domaine et/ou adresses IP ce bloc de serveur doit répondre. Pointez cette directive vers le nom de domaine de votre serveur ou l'adresse IP publique.
location / — Le premier bloc de localisation inclut une directive try_files, qui vérifie l'existence de fichiers ou de répertoires correspondant à une requête URI. Si Nginx ne trouve pas la ressource appropriée, il renverra une erreur 404.
location ~ .php$ — Ce bloc de localisation gère le traitement réel de PHP en pointant Nginx vers le fichier de configuration fastcgi-php.conf et le fichier php7.4-fpm.sock, qui déclare quel socket est associé à php-fpm.
location ~ /.ht — Le dernier bloc de localisation s'occupe des fichiers .htaccess, que Nginx ne traite pas. En ajoutant la directive deny all, si des fichiers .htaccess parviennent à trouver leur chemin dans le répertoire racine, ils ne seront pas servis aux visiteurs.
Lorsque vous avez terminé d'éditer, enregistrez et fermez le fichier. Si vous utilisez nano, vous pouvez le faire en tapant CTRL+X, puis y et ENTRER pour confirmer.

Activez votre configuration en créant un lien vers le fichier de configuration à partir du répertoire sites-enabled de Nginx :

```
sudo ln -s /etc/nginx/sites-available/projectLEMP /etc/nginx/sites-enabled/
```

Cela indiquera à Nginx d'utiliser la configuration lors du prochain rechargement. Vous pouvez tester votre configuration pour les erreurs de syntaxe en tapant :

```
sudo nginx -t
```

Vous devriez voir le message suivant :

```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
Si des erreurs sont signalées, retournez dans votre fichier de configuration pour examiner son contenu avant de continuer.

Nous devons également désactiver l'hôte Nginx par défaut qui est actuellement configuré pour écouter sur le port 80. Pour cela, exécutez :
```
sudo unlink /etc/nginx/sites-enabled/default
```

Lorsque vous êtes prêt, rechargez Nginx pour appliquer les modifications :

```
sudo systemctl reload nginx
```

Votre nouveau site web est maintenant actif, mais le répertoire racine /var/www/projectLEMP est toujours vide. Créez un fichier index.html à cet emplacement afin que nous puissions tester que votre nouveau bloc de serveur fonctionne comme prévu :


Maintenant, allez dans votre navigateur et essayez d'ouvrir l'URL de votre site web en utilisant l'adresse IP :
```
http://<Public-IP-Address>:80
```

<img width="1435" alt="Capture d’écran 2024-10-09 à 12 03 35" src="https://github.com/user-attachments/assets/aa789325-d0b1-4f84-b36e-60f821a7fe1f">


Vous pouvez laisser ce fichier en place comme une page de destination temporaire pour votre application jusqu'à ce que vous configuriez un fichier index.php pour le remplacer. Une fois que vous aurez fait cela, n'oubliez pas de supprimer ou de renommer le fichier index.html de votre répertoire racine, car il aurait par défaut la priorité sur un fichier index.php.

Votre pile LEMP est maintenant entièrement configurée. À l'étape suivante, nous allons créer un script PHP pour tester que Nginx est en effet capable de gérer les fichiers .php au sein de votre site nouvellement configuré.

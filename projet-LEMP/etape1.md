# STEP 1 – INSTALLATION DU SERVEUR WEB NGINX

Afin d'afficher des pages Web à nos visiteurs, nous allons utiliser Nginx, un serveur web haute performance. Nous allons utiliser le gestionnaire de paquets apt pour installer ce package.

Comme c'est notre première fois en utilisant apt pour cette session, commençons par mettre à jour l'index des paquets de votre serveur. 

Ensuite, vous pouvez utiliser apt install pour installer Nginx :

```
sudo apt update
sudo apt install nginx
```
Lorsque vous y êtes invité, entrez Y pour confirmer que vous souhaitez installer Nginx. Une fois l'installation terminée, le serveur web Nginx sera actif et en cours d'exécution sur votre serveur Ubuntu 22.04.

Pour vérifier que Nginx a été installé avec succès et fonctionne en tant que service sur Ubuntu, exécutez :

```
sudo systemctl status nginx
```

S'il est en vert et en cours d'exécution, alors vous avez tout fait correctement – vous venez de lancer votre premier serveur Web dans le Cloud !


Tout d'abord, essayons de vérifier comment nous pouvons y accéder localement dans notre shell Ubuntu, exécutez :
```
curl http://localhost:80
or
curl http://127.0.0.1:80
```

L'URL dans le navigateur fonctionnera également si vous ne spécifiez pas le numéro de port, car tous les navigateurs web utilisent le port 80 par défaut.

Si vous voyez la page suivante, alors votre serveur web est maintenant correctement installé et accessible via votre pare-feu.

![projje2-step0](https://user-images.githubusercontent.com/85270361/210116186-f5ec30cf-5fe3-410d-9c21-2f26b03c4815.PNG)

En fait, c'est le même contenu que vous avez précédemment obtenu par la commande curl, mais représenté dans un beau format HTML par votre navigateur web.

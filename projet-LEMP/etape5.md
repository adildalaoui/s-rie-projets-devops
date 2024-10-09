# STEP 5 – TEST DE PHP AVEC NGINX

Votre pile LEMP devrait maintenant être complètement configurée.

À ce stade, votre pile LAMP est entièrement installée et opérationnelle.

Vous pouvez la tester pour valider que Nginx peut correctement transmettre les fichiers .php à votre processeur PHP.

Pour cela, vous pouvez créer un fichier PHP de test dans votre répertoire racine. 
Ouvrez un nouveau fichier appelé info.php dans votre répertoire racine avec votre éditeur de texte :

```
sudo nano /var/www/projectLEMP/info.php
```

Tapez ou collez les lignes suivantes dans le nouveau fichier. 
Ceci est un code PHP valide qui renverra des informations sur votre serveur :

```
<?php
phpinfo();
```
Vous pouvez maintenant accéder à cette page dans votre navigateur web en visitant le nom de domaine ou l'adresse IP publique que vous avez configuré dans votre fichier de configuration Nginx, suivi de /info.php :

```
http://`server_domain_or_IP`/info.php
```

Vous verrez une page web contenant des informations détaillées sur votre serveur :

![projject1-step5](https://user-images.githubusercontent.com/85270361/210117729-d93d8aad-b131-40c2-b28d-ca0289327906.PNG)

Après avoir vérifié les informations pertinentes sur votre serveur PHP via cette page, il est préférable de supprimer le fichier que vous avez créé, car il contient des informations sensibles sur votre environnement PHP et votre serveur Ubuntu.
Vous pouvez utiliser rm pour supprimer ce fichier 

```
sudo rm /var/www/your_domain/info.php
```

Vous pouvez toujours régénérer ce fichier si vous en avez besoin plus tard.

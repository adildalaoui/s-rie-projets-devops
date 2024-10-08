# STEP 3 — INSTALLATION  

Vous avez installé Apache pour servir votre contenu et MySQL pour stocker et gérer vos données. PHP est le composant de notre configuration qui va traiter le code afin d'afficher du contenu dynamique à l'utilisateur final. En plus du paquet PHP, vous aurez besoin de php-mysql, un module PHP qui permet à PHP de communiquer avec des bases de données MySQL. Vous aurez également besoin de libapache2-mod-php pour permettre à Apache de gérer les fichiers PHP. Les paquets principaux de PHP seront installés automatiquement comme dépendances.

Pour installer ces 3 paquets en une seule commande, exécutez :

```
sudo apt install php libapache2-mod-php php-mysql
```

Une fois l'installation terminée, vous pouvez exécuter la commande suivante pour confirmer la version de PHP :
```
php -v
```

```
PHP 7.4.3 (cli) (built: Oct  6 2020 15:47:56) ( NTS )
Copyright (c) The PHP Group
Zend Engine v3.4.0, Copyright (c) Zend Technologies
```

À ce stade, votre pile LAMP est entièrement installée et opérationnelle.

- Linux (Ubuntu)
- Serveur HTTP Apache
- MySQL
- PHP
  
Pour tester votre configuration avec un script PHP, il est préférable de configurer un hôte virtuel Apache adéquat pour héberger les fichiers et dossiers de votre site web. L'hôte virtuel permet d'héberger plusieurs sites sur une seule machine, et les utilisateurs des sites ne s'en apercevront même pas.

Nous allons configurer notre premier hôte virtuel à l'étape suivante.

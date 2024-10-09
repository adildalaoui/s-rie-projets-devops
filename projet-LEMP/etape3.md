# STEP 3 – INSTALLATION DE PHP

Vous avez installé Nginx pour servir votre contenu et MySQL pour stocker et gérer vos données. Maintenant, vous pouvez installer PHP pour traiter le code et générer du contenu dynamique pour le serveur web.

Alors qu'Apache intègre l'interpréteur PHP dans chaque requête, Nginx nécessite un programme externe pour gérer le traitement PHP et agir comme un pont entre l'interpréteur PHP lui-même et le serveur web. Cela permet une meilleure performance globale dans la plupart des sites web basés sur PHP, mais cela nécessite une configuration supplémentaire. Vous devrez installer php-fpm, qui signifie "PHP FastCGI Process Manager", et indiquer à Nginx de passer les requêtes PHP à ce logiciel pour traitement. De plus, vous aurez besoin de php-mysql, un module PHP qui permet à PHP de communiquer avec des bases de données basées sur MySQL. Les paquets PHP de base seront automatiquement installés comme dépendances.

Pour installer ces 2 paquets en une seule commande, exécutez :

```
sudo apt install php-fpm php-mysql
```
Lorsque vous y êtes invité, tapez Y et appuyez sur ENTRER pour confirmer l'installation.

Vous avez maintenant vos composants PHP installés. Ensuite, vous allez configurer Nginx pour les utiliser.

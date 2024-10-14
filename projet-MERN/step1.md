# STEP 1 – BACKEND CONFIGURATION

Mettre à jour ubuntu

```
sudo apt update
```

Mettre à niveau ubuntu

```
sudo apt upgrade
```

Obtention de l'emplacement du logiciel Node.js à partir des dépôts Ubuntu.

```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```

Installer Node.js sur le serveur.
Installez Node.js avec la commande ci-dessous.

```
sudo apt-get install -y nodejs
```

Remarque : La commande ci-dessus installe à la fois Node.js et npm. NPM est un gestionnaire de paquets pour Node, comme apt pour Ubuntu. Il est utilisé pour installer des modules et des paquets Node, ainsi que pour gérer les conflits de dépendances.

Vérifiez l'installation de Node avec la commande ci-dessous.

```
node -v 
```

Vérifiez l'installation de Npm avec la commande ci-dessous

```
npm -v
```

Configuration du code de l'application
Créez un nouveau répertoire pour votre projet de liste de tâches (To-Do) :

```
mkdir Todo
```


Maintenant, changez votre répertoire actuel pour celui que vous venez de créer :

```
cd Todo
```

Ensuite, vous utiliserez la commande npm init pour initialiser votre projet, afin qu'un nouveau fichier nommé package.json soit créé. Ce fichier contiendra normalement des informations sur votre application et les dépendances nécessaires à son exécution. Suivez les instructions après avoir exécuté la commande. Vous pouvez appuyer sur Entrée plusieurs fois pour accepter les valeurs par défaut, puis accepter d'enregistrer le fichier package.json en tapant "yes."

```
npm init
```

Exécutez la commande ls pour confirmer que le fichier package.json a été créé.

Ensuite, nous allons installer Express.js et créer le répertoire Routes.

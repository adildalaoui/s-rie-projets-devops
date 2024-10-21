Maintenant que vous avez déjà appris à déployer les piles Web LAMP, LEMP et MERN, il est temps de vous familiariser avec la pile MEAN et de la déployer sur un serveur Ubuntu.

La pile MEAN est une combinaison des composants suivants :

- MongoDB (Base de données de documents) – Stocke et permet de récupérer les données.
- Express (Cadre d'application back-end) – Effectue des requêtes vers la base de données pour les lectures et écritures.
- Angular (Cadre d'application front-end) – Gère les requêtes client et serveur.
- Node.js (Environnement d'exécution JavaScript) – Accepte les requêtes et affiche les résultats à l'utilisateur final.


Auto-apprentissage complémentaire:
- Rafraîchissez vos connaissances sur le modèle OSI.
- Lisez sur l'équilibrage de charge (Load Balancing) et familiarisez-vous avec les différents types et techniques d'équilibrage de la charge du trafic.
- Entraînez-vous à modifier de simples formulaires web avec HTML + CSS + JS.
- Instructions pour soumettre votre travail pour révision et feedback
Pour soumettre votre travail pour révision et feedback, suivez cette instruction.

Étape 0 – Préparation des prérequis

Pour compléter ce projet, vous aurez besoin d'un compte AWS et d'un serveur virtuel avec le système d'exploitation Ubuntu Server.

Si vous n'avez pas de compte AWS, retournez à l'étape 0 du projet 1 pour vous inscrire à un compte gratuit AWS et créez une nouvelle instance EC2 de la famille t2.nano avec l'image Ubuntu Server 20.04 LTS (HVM). Rappelez-vous, vous pouvez avoir plusieurs instances EC2, mais assurez-vous de STOPPER celles que vous n'utilisez pas actuellement afin de préserver les heures gratuites disponibles.

Astuce : Dans les projets précédents, nous avons utilisé différents outils pour nous connecter à une instance EC2, mais si vous ne voulez pas installer ou lancer quoi que ce soit en dehors d'AWS, vous pouvez ouvrir votre interface de ligne de commande (CLI) directement depuis la console Web dans AWS, de cette manière :


![5013](https://user-images.githubusercontent.com/85270361/210133716-47e26536-6479-440d-9c15-981cab3bbaac.PNG)

Tâche
Dans cet exercice, vous allez implémenter un simple formulaire d'enregistrement de livres en utilisant la pile MEAN.

Étape 1 : Installer Node.js

Node.js est un environnement d'exécution JavaScript basé sur le moteur JavaScript V8 de Chrome.
Node.js sera utilisé dans ce tutoriel pour configurer les routes Express et les contrôleurs AngularJS.
Update ubuntu

```
sudo apt update
```

Upgrade ubuntu

```
sudo apt upgrade
```

Ajoutez des certificats

```
sudo apt -y install curl dirmngr apt-transport-https lsb-release ca-certificates

curl -sL https://deb.nodesource.com/setup_12.x | sudo -E bash -
```

Installer NodeJS

```
sudo apt install -y nodejs
```

Étape 2 : Installer MongoDB

MongoDB stocke les données dans des documents flexibles, similaires à du JSON. Les champs dans une base de données peuvent varier d'un document à l'autre, et la structure des données peut être modifiée au fil du temps. Pour notre application d'exemple, nous allons ajouter des enregistrements de livres dans MongoDB qui contiennent le nom du livre, le numéro ISBN, l'auteur et le nombre de pages.


```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
```

```
echo "deb [ arch=amd64 ] https://repo.mongodb.org/apt/ubuntu trusty/mongodb-org/3.4 multiverse" |
sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```

Installer MongoDB

```
sudo apt install -y mongodb
```

Démarrer le serveur.

```
sudo service mongodb start
```

Vérifiez que le service est opérationnel

```
sudo systemctl status mongodb
```

Installer npm – Node package manager.

```
sudo apt install -y npm
```

Installez le paquet body-parser

Nous avons besoin du paquet 'body-parser' pour nous aider à traiter les fichiers JSON envoyés dans les requêtes au serveur

```
sudo npm install body-parser
```

Créez un dossier nommé « Books »

```
mkdir Books && cd Books
```

Dans le répertoire Books, initialisez le projet npm.

```
npm init
```

Ajoutez-y un fichier nommé server.js.

```
vi server.js
```

Copiez et collez le code du serveur web ci-dessous dans le fichier server.js.

```
var express = require('express');
var bodyParser = require('body-parser');
var app = express();
app.use(express.static(__dirname + '/public'));
app.use(bodyParser.json());
require('./apps/routes')(app);
app.set('port', 3300);
app.listen(app.get('port'), function() {
    console.log('Server up: http://localhost:' + app.get('port'));
});
```


# INSTALLER EXPRESS ET CONFIGURER LES ROUTES DU SERVEUR

Étape 3 : Installer Express et configurer les routes du serveur

Express est un framework d'application web Node.js minimal et flexible qui fournit des fonctionnalités pour les applications web et mobiles. Nous allons utiliser Express pour transférer les informations sur les livres vers et depuis notre base de données MongoDB.

Nous allons également utiliser le paquet Mongoose, qui offre une solution simple et basée sur un schéma pour modéliser les données de votre application. Nous utiliserons Mongoose pour établir un schéma pour la base de données afin de stocker les données de notre registre de livres.

```
sudo npm install express mongoose
```

Dans le dossier Books, créez un dossier nommé apps

```
mkdir apps && cd apps
```

Créez un fichier nommé routes.js.

```
vi routes.js
```

Copiez et collez le code ci-dessous dans routes.js.

```
var Book = require('./models/book');
module.exports = function(app) {
  app.get('/book', function(req, res) {
    Book.find({}, function(err, result) {
      if ( err ) throw err;
      res.json(result);
    });
  }); 
  app.post('/book', function(req, res) {
    var book = new Book( {
      name:req.body.name,
      isbn:req.body.isbn,
      author:req.body.author,
      pages:req.body.pages
    });
    book.save(function(err, result) {
      if ( err ) throw err;
      res.json( {
        message:"Successfully added book",
        book:result
      });
    });
  });
  app.delete("/book/:isbn", function(req, res) {
    Book.findOneAndRemove(req.query, function(err, result) {
      if ( err ) throw err;
      res.json( {
        message: "Successfully deleted the book",
        book: result
      });
    });
  });
  var path = require('path');
  app.get('*', function(req, res) {
    res.sendfile(path.join(__dirname + '/public', 'index.html'));
  });
};
```

Dans le dossier apps, créez un dossier nommé models.

```
mkdir models && cd models
```

Créez un fichier nommé book.js.

```
vi book.js
```

Copiez et collez le code ci-dessous dans book.js.

```
var mongoose = require('mongoose');
var dbHost = 'mongodb://localhost:27017/test';
mongoose.connect(dbHost);
mongoose.connection;
mongoose.set('debug', true);
var bookSchema = mongoose.Schema( {
  name: String,
  isbn: {type: String, index: true},
  author: String,
  pages: Number
});
var Book = mongoose.model('Book', bookSchema);
module.exports = mongoose.model('Book', bookSchema);
```

Étape 4 – Accéder aux routes avec AngularJS

AngularJS fournit un framework web pour créer des vues dynamiques dans vos applications web. Dans ce tutoriel, nous utilisons AngularJS pour connecter notre page web à Express et effectuer des actions sur notre registre de livres.

Changez le répertoire pour revenir à Books.

```
cd ../..
```

Créez un dossier nommé public.

```
mkdir public && cd public
```

Ajoutez un fichier nommé script.js

```
vi script.js
```

Copiez et collez le code ci-dessous (configuration du contrôleur définie) dans le fichier script.js.

```
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $http) {
  $http( {
    method: 'GET',
    url: '/book'
  }).then(function successCallback(response) {
    $scope.books = response.data;
  }, function errorCallback(response) {
    console.log('Error: ' + response);
  });
  $scope.del_book = function(book) {
    $http( {
      method: 'DELETE',
      url: '/book/:isbn',
      params: {'isbn': book.isbn}
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
  $scope.add_book = function() {
    var body = '{ "name": "' + $scope.Name + 
    '", "isbn": "' + $scope.Isbn +
    '", "author": "' + $scope.Author + 
    '", "pages": "' + $scope.Pages + '" }';
    $http({
      method: 'POST',
      url: '/book',
      data: body
    }).then(function successCallback(response) {
      console.log(response);
    }, function errorCallback(response) {
      console.log('Error: ' + response);
    });
  };
});
```

Dans le dossier public, créez un fichier nommé index.html.

```
vi index.html
```

Copiez et collez le code ci-dessous dans le fichier index.html.


```
<!doctype html>
<html ng-app="myApp" ng-controller="myCtrl">
  <head>
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.4/angular.min.js"></script>
    <script src="script.js"></script>
  </head>
  <body>
    <div>
      <table>
        <tr>
          <td>Name:</td>
          <td><input type="text" ng-model="Name"></td>
        </tr>
        <tr>
          <td>Isbn:</td>
          <td><input type="text" ng-model="Isbn"></td>
        </tr>
        <tr>
          <td>Author:</td>
          <td><input type="text" ng-model="Author"></td>
        </tr>
        <tr>
          <td>Pages:</td>
          <td><input type="number" ng-model="Pages"></td>
        </tr>
      </table>
      <button ng-click="add_book()">Add</button>
    </div>
    <hr>
    <div>
      <table>
        <tr>
          <th>Name</th>
          <th>Isbn</th>
          <th>Author</th>
          <th>Pages</th>

        </tr>
        <tr ng-repeat="book in books">
          <td>{{book.name}}</td>
          <td>{{book.isbn}}</td>
          <td>{{book.author}}</td>
          <td>{{book.pages}}</td>

          <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
        </tr>
      </table>
    </div>
  </body>
</html>
```

Changez le répertoire pour remonter à Books.

```
cd ..
```

Démarrez le serveur en exécutant cette commande :

```
node server.js
```

Le serveur est maintenant opérationnel. Nous pouvons nous y connecter via le port 3300. Vous pouvez lancer une console Putty ou SSH séparée pour tester ce que la commande curl retourne localement.

```
curl -s http://localhost:3300
```

Cela devrait retourner une page HTML, qui est difficilement lisible dans l'interface de ligne de commande (CLI), mais nous pouvons également essayer d'y accéder depuis Internet.

Pour cela, vous devez ouvrir le port TCP 3300 dans votre console web AWS pour votre instance EC2.

Vous êtes censé savoir comment le faire ; si vous avez oublié, référez-vous au Projet 1 (Étape 1 — Installation d'Apache et mise à jour du pare-feu).



Maintenant, vous pouvez accéder à notre application web d'enregistrement de livres depuis Internet avec un navigateur en utilisant l'adresse IP publique ou le nom DNS public.

Petit rappel sur la façon d'obtenir l'adresse IP publique et le nom DNS public de votre serveur :

Vous pouvez le trouver dans votre console web AWS dans les détails de l'EC2 :

Exécutez curl -s http://169.254.169.254/latest/meta-data/public-ipv4 pour obtenir l'adresse IP publique ou
curl -s http://169.254.169.254/latest/meta-data/public-hostname pour obtenir le nom DNS public.
Voici à quoi ressemblera votre application Web d'enregistrement de livres dans le navigateur :

<img width="1430" alt="Capture d’écran 2024-10-16 à 12 39 01" src="https://github.com/user-attachments/assets/a243c265-4cac-4959-b709-6a8bfbcb1435">


Félicitations !
Vous avez maintenant terminé tous les projets « PBL Progressifs » et êtes prêt à passer à des projets « PBL Professionnels » plus complexes et amusants !







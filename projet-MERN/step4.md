# BASE DE DONNÉES MONGODB

Nous avons besoin d'une base de données où nous stockerons nos données. Pour cela, nous allons utiliser mLab. mLab fournit une solution de base de données MongoDB en tant que service (DBaaS), donc pour vous faciliter la vie, vous devrez vous inscrire pour un compte gratuit de clusters partagés, ce qui est idéal pour notre cas d'utilisation.
Inscrivez-vous ici. Suivez le processus d'inscription, sélectionnez AWS comme fournisseur de cloud et choisissez une région près de chez vous.

Complétez une liste de vérification pour commencer, comme indiqué sur l'image ci-dessous.

![5003](https://user-images.githubusercontent.com/85270361/210130940-3d8a93d0-d7e1-46d6-87bc-57deaa5ac417.PNG)

Autorisez l'accès à la base de données MongoDB depuis n'importe où (ce n'est pas sécurisé, mais c'est idéal pour les tests).

REMARQUE IMPORTANTE
Dans l'image ci-dessous, assurez-vous de changer le temps de suppression de l'entrée de 6 heures à 1 semaine.


![5004](https://user-images.githubusercontent.com/85270361/210130965-09bfdbb5-8ca1-46ad-bc10-37d0a8ac54db.PNG)


Créez une base de données MongoDB et une collection à l'intérieur de mLab.


![5005](https://user-images.githubusercontent.com/85270361/210130999-ae626111-3e54-4273-a194-e447662f19e0.PNG)


Dans le fichier index.js, nous avons spécifié process.env pour accéder aux variables d'environnement, mais nous n'avons pas encore créé ce fichier. Nous devons donc le faire maintenant.

Créez un fichier dans votre répertoire Todo et nommez-le .env.

```
touch .env
vi .env
```

Ajoutez la chaîne de connexion pour accéder à la base de données dans ce fichier, comme ci-dessous :

```
DB = 'mongodb+srv://<username>:<password>@<network-address>/<dbname>?retryWrites=true&w=majority'
```

Assurez-vous de mettre à jour <username>, <password>, <network-address> et <database> selon votre configuration.

Voici comment obtenir votre chaîne de connexion :
  
![5006](https://user-images.githubusercontent.com/85270361/210131129-c22696a1-76bb-41cf-a6cf-5028c7ab6845.PNG)

  
![50007](https://user-images.githubusercontent.com/85270361/210131217-788a794c-8e51-49fa-8a00-35e7b8982e16.PNG)

  
 Maintenant, nous devons mettre à jour le fichier index.js pour refléter l'utilisation de .env afin que Node.js puisse se connecter à la base de données.

Supprimez simplement le contenu existant dans le fichier et mettez-le à jour avec tout le code ci-dessous.

Pour ce faire en utilisant vim, suivez les étapes ci-dessous :

Ouvrez le fichier avec vim index.js
Appuyez sur Esc
Tapez :
Tapez %d
Appuyez sur Entrée
Tout le contenu sera supprimé, puis :

Appuyez sur i pour entrer en mode d'insertion dans vim
Maintenant, collez tout le code ci-dessous dans le fichier.
  

```
const express = require('express');
const bodyParser = require('body-parser');
const mongoose = require('mongoose');
const routes = require('./routes/api');
const path = require('path');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

//connect to the database
mongoose.connect(process.env.DB, { useNewUrlParser: true, useUnifiedTopology: true })
.then(() => console.log(`Database connected successfully`))
.catch(err => console.log(err));

//since mongoose promise is depreciated, we overide it with node's promise
mongoose.Promise = global.Promise;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use(bodyParser.json());

app.use('/api', routes);

app.use((err, req, res, next) => {
console.log(err);
next();
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
```

Utiliser des variables d'environnement pour stocker des informations est considéré comme plus sûr et est la meilleure pratique pour séparer la configuration et les données sensibles de l'application, au lieu d'écrire les chaînes de connexion directement dans le fichier de l'application index.js.

Démarrez votre serveur en utilisant la commande :
  
```
node index.js
```
  
 
Vous devriez voir un message "Database connected successfully". Si c'est le cas, nous avons configuré notre backend. Maintenant, nous allons le tester.

Tester le code backend sans interface frontend en utilisant l'API RESTful
Jusqu'à présent, nous avons écrit la partie backend de notre application To-Do et configuré une base de données, mais nous n'avons pas encore d'interface utilisateur frontend. Nous avons besoin de code ReactJS pour cela. Mais pendant le développement, nous aurons besoin d'un moyen de tester notre code en utilisant l'API RESTful. Par conséquent, nous devrons utiliser un client de développement API pour tester notre code.

Dans ce projet, nous allons utiliser Postman pour tester notre API. Cliquez sur Install Postman pour télécharger et installer Postman sur votre machine.

Cliquez ICI pour apprendre comment effectuer des opérations CRUD sur Postman.

Vous devez tester tous les points de terminaison de l'API et vous assurer qu'ils fonctionnent. Pour les points de terminaison qui nécessitent un corps, vous devez envoyer un JSON avec les champs nécessaires, car c'est ce que nous avons configuré dans notre code.

Maintenant, ouvrez Postman, créez une requête POST vers l'API http://<PublicIP-or-PublicDNS>:5000/api/todos. Cette requête envoie une nouvelle tâche à notre liste To-Do afin que l'application puisse l'enregistrer dans la base de données.

Remarque : assurez-vous de définir l'en-tête Content-Type sur application/json.
 
 
![5008](https://user-images.githubusercontent.com/85270361/210131561-9316f8f5-2112-4f09-846a-544677328817.PNG)

Vérifiez l'image ci-dessous :
  
  
![5009](https://user-images.githubusercontent.com/85270361/210131585-627646c4-a59e-48c3-8edd-0354e4ac2431.PNG)


Créez une requête GET vers votre API à l'adresse http://<PublicIP-or-PublicDNS>:5000/api/todos.
Cette requête récupère tous les enregistrements existants de notre application To-Do (le backend demande ces enregistrements à la base de données et nous les renvoie en réponse à la requête GET).
  
![5010](https://user-images.githubusercontent.com/85270361/210131610-9c7c4544-1e2b-40f3-b2b6-bcd389857b0d.PNG)

  
Tâche optionnelle : Essayez de découvrir comment envoyer une requête DELETE pour supprimer une tâche de notre liste To-Do.

Indice : Pour supprimer une tâche, vous devez envoyer son ID en tant que partie de la requête DELETE.

Désormais, vous avez testé la partie backend de notre application To-Do et vous vous êtes assuré qu'elle prend en charge les trois opérations que nous souhaitions :

Afficher une liste de tâches – requête HTTP GET
Ajouter une nouvelle tâche à la liste – requête HTTP POST
Supprimer une tâche existante de la liste – requête HTTP DELETE
Nous avons réussi à créer notre backend, maintenant allons créer le frontend.

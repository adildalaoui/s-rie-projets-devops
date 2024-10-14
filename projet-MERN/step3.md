# MODÈLES

Maintenant, vient la partie intéressante, car l'application va utiliser MongoDB, qui est une base de données NoSQL. Nous devons donc créer un modèle.

Un modèle est au cœur des applications basées sur JavaScript, et c'est ce qui les rend interactives.

Nous utiliserons également des modèles pour définir le schéma de la base de données. Cela est important afin que nous puissions définir les champs stockés dans chaque document MongoDB. (Cela semble être beaucoup d'informations, mais ne vous inquiétez pas, tout deviendra clair pour vous avec le temps. Je vous le promets !)

En essence, le schéma est un plan de la façon dont la base de données sera construite, y compris d'autres champs de données qui peuvent ne pas être nécessaires à stocker dans la base de données. Ceux-ci sont connus sous le nom de propriétés virtuelles.

Pour créer un schéma et un modèle, installez Mongoose, qui est un paquet Node.js qui facilite le travail avec MongoDB.

Changez de répertoire pour revenir au dossier Todo avec cd .. et installez Mongoose.

```
npm install mongoose
```

Créez un nouveau dossier models :


```
mkdir models
```

Changez de répertoire pour entrer dans le dossier models nouvellement créé avec :


```
cd models
```

À l'intérieur du dossier models, créez un fichier et nommez-le todo.js.


```
touch todo.js
```

Ouvrez le fichier créé avec vim todo.js, puis collez le code ci-dessous dans le fichier :

```
const mongoose = require('mongoose');
const Schema = mongoose.Schema;

//create schema for todo
const TodoSchema = new Schema({
action: {
type: String,
required: [true, 'The todo text field is required']
}
})

//create model for todo
const Todo = mongoose.model('todo', TodoSchema);

module.exports = Todo;
```


Maintenant, nous devons mettre à jour nos routes dans le fichier api.js dans le répertoire routes pour utiliser le nouveau modèle.

Dans le répertoire routes, ouvrez api.js avec vim api.js, supprimez le code à l'intérieur avec la commande :%d et collez le code ci-dessous dedans, puis enregistrez et quittez :


```
const express = require ('express');
const router = express.Router();
const Todo = require('../models/todo');

router.get('/todos', (req, res, next) => {

//this will return all the data, exposing only the id and action field to the client
Todo.find({}, 'action')
.then(data => res.json(data))
.catch(next)
});

router.post('/todos', (req, res, next) => {
if(req.body.action){
Todo.create(req.body)
.then(data => res.json(data))
.catch(next)
}else {
res.json({
error: "The input field is empty"
})
}
});

router.delete('/todos/:id', (req, res, next) => {
Todo.findOneAndDelete({"_id": req.params.id})
.then(data => res.json(data))
.catch(next)
})

module.exports = router;
```

La prochaine partie de notre application sera la base de données MongoDB.

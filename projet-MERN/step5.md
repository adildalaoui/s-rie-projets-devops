STEP 5 – CREATION du  FRONTEND

Puisque nous avons terminé avec les fonctionnalités que nous voulons pour notre backend et notre API, il est temps de créer une interface utilisateur pour un client Web (navigateur) afin d'interagir avec l'application via l'API. Pour commencer avec le frontend de l'application To-Do, nous utiliserons la commande create-react-app pour générer la structure de notre application.

Dans le même répertoire racine que votre code backend, c'est-à-dire le répertoire Todo, exécutez :

```
npx create-react-app client
```

Cela créera un nouveau dossier dans votre répertoire Todo appelé client, où vous ajouterez tout le code React.

Exécution d'une application React
Avant de tester l'application React, certaines dépendances doivent être installées.

Installez concurrently. Il est utilisé pour exécuter plusieurs commandes simultanément à partir de la même fenêtre de terminal.

```
npm install concurrently --save-dev
```

2. Installez nodemon. Il est utilisé pour exécuter et surveiller le serveur. Si une modification est apportée au code du serveur, nodemon le redémarrera automatiquement et chargera les nouveaux changements.


```
npm install nodemon --save-dev
```

3. Dans le dossier Todo, ouvrez le fichier package.json. Modifiez la partie mise en évidence de la capture d'écran ci-dessous et remplacez-la par le code suivant.

```
"scripts": {
"start": "node index.js",
"start-watch": "nodemon index.js",
"dev": "concurrently \"npm run start-watch\" \"cd client && npm start\""
},
```


![5011](https://user-images.githubusercontent.com/85270361/210131756-fea4a40b-e23c-4937-997f-bc8d022bf763.PNG)


Configurer le proxy dans package.json

Changez de répertoire pour aller dans le dossier client.

```
cd client
```

2. Ouvrez le fichier package.json.

```
vi package.json
```

3. Ajoutez la paire clé-valeur suivante dans le fichier package.json : "proxy": "http://localhost:5000".

L'objectif de l'ajout de la configuration de proxy dans le point 3 ci-dessus est de permettre d'accéder directement à l'application depuis le navigateur en appelant simplement l'URL du serveur comme http://localhost:5000 plutôt que d'inclure toujours tout le chemin comme http://localhost:5000/api/todos.

Maintenant, assurez-vous d'être dans le répertoire Todo, puis faites simplement :

```
npm run dev
```

Votre application devrait s'ouvrir et commencer à fonctionner sur localhost:3000.

Note importante : Pour pouvoir accéder à l'application depuis Internet, vous devez ouvrir le port TCP 3000 sur EC2 en ajoutant une nouvelle règle de groupe de sécurité. Vous savez déjà comment le faire.

Création de vos composants React
L'un des avantages de React est qu'il utilise des composants, qui sont réutilisables et rendent également le code modulaire. Pour notre application Todo, il y aura deux composants à état (stateful components) et un composant sans état (stateless component).

Depuis votre répertoire Todo, exécutez :


```
cd client
```

Déplacez-vous dans le répertoire src.

```
cd src
```

À l'intérieur de votre dossier src, créez un autre dossier appelé components.

```
mkdir components
```

Déplacez-vous dans le répertoire components avec :

```
cd components
```

À l'intérieur du répertoire components, créez trois fichiers : Input.js, ListTodo.js et Todo.js.

```
touch Input.js ListTodo.js Todo.js
```

Ouvrez le fichier Input.js

```
vi Input.js
```

Copiez et collez ce qui suit :

```
import React, { Component } from 'react';
import axios from 'axios';

class Input extends Component {

state = {
action: ""
}

addTodo = () => {
const task = {action: this.state.action}

    if(task.action && task.action.length > 0){
      axios.post('/api/todos', task)
        .then(res => {
          if(res.data){
            this.props.getTodos();
            this.setState({action: ""})
          }
        })
        .catch(err => console.log(err))
    }else {
      console.log('input field required')
    }

}

handleChange = (e) => {
this.setState({
action: e.target.value
})
}

render() {
let { action } = this.state;
return (
<div>
<input type="text" onChange={this.handleChange} value={action} />
<button onClick={this.addTodo}>add todo</button>
</div>
)
}
}

export default Input
```


Pour utiliser Axios, qui est un client HTTP basé sur les promesses pour le navigateur et Node.js, vous devez vous rendre dans votre dossier client depuis votre terminal et exécuter yarn add axios ou npm install axios.

Déplacez-vous ensuite dans le dossier src.

```
cd ..
```

Déplacez-vous dans le dossier client

```
cd ..
```

Installer Axios

```
npm install axios
```

Sirotez un café, cliquez sur le bouton suivant et terminons cela.

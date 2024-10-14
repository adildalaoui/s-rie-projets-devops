# CRÉATION DU FRONTEND (CONTINUÉE)

Allez dans le répertoire components.

```
cd src/components
```

Après cela, ouvrez votre fichier ListTodo.js

```
vi ListTodo.js
```

Dans le fichier ListTodo.js, copiez et collez le code suivant :

```
import React from 'react';

const ListTodo = ({ todos, deleteTodo }) => {

return (
<ul>
{
todos &&
todos.length > 0 ?
(
todos.map(todo => {
return (
<li key={todo._id} onClick={() => deleteTodo(todo._id)}>{todo.action}</li>
)
})
)
:
(
<li>No todo(s) left</li>
)
}
</ul>
)
}

export default ListTodo
```


Ensuite, dans votre fichier Todo.js, écrivez le code suivant :

```
import React, {Component} from 'react';
import axios from 'axios';

import Input from './Input';
import ListTodo from './ListTodo';

class Todo extends Component {

state = {
todos: []
}

componentDidMount(){
this.getTodos();
}

getTodos = () => {
axios.get('/api/todos')
.then(res => {
if(res.data){
this.setState({
todos: res.data
})
}
})
.catch(err => console.log(err))
}

deleteTodo = (id) => {

    axios.delete(`/api/todos/${id}`)
      .then(res => {
        if(res.data){
          this.getTodos()
        }
      })
      .catch(err => console.log(err))

}

render() {
let { todos } = this.state;

    return(
      <div>
        <h1>My Todo(s)</h1>
        <Input getTodos={this.getTodos}/>
        <ListTodo todos={todos} deleteTodo={this.deleteTodo}/>
      </div>
    )

}
}

export default Todo;
```


Nous devons apporter quelques ajustements à notre code React. Supprimez le logo et ajustez notre App.js pour qu'il ressemble à ceci.

Déplacez-vous dans le dossier src.


```
cd ..
```

Assurez-vous d'être dans le dossier src et exécutez :

```
vi App.js
```

Copiez et collez le code ci-dessous dans le fichier :


```
import React from 'react';

import Todo from './components/Todo';
import './App.css';

const App = () => {
return (
<div className="App">
<Todo />
</div>
);
}

export default App;
```

Après avoir collé le code, quittez l'éditeur.

Dans le répertoire src, ouvrez le fichier App.css


```
vi App.css
```

Ensuite, collez le code suivant dans App.css :


```
.App {
text-align: center;
font-size: calc(10px + 2vmin);
width: 60%;
margin-left: auto;
margin-right: auto;
}

input {
height: 40px;
width: 50%;
border: none;
border-bottom: 2px #101113 solid;
background: none;
font-size: 1.5rem;
color: #787a80;
}

input:focus {
outline: none;
}

button {
width: 25%;
height: 45px;
border: none;
margin-left: 10px;
font-size: 25px;
background: #101113;
border-radius: 5px;
color: #787a80;
cursor: pointer;
}

button:focus {
outline: none;
}

ul {
list-style: none;
text-align: left;
padding: 15px;
background: #171a1f;
border-radius: 5px;
}

li {
padding: 15px;
font-size: 1.5rem;
margin-bottom: 15px;
background: #282c34;
border-radius: 5px;
overflow-wrap: break-word;
cursor: pointer;
}

@media only screen and (min-width: 300px) {
.App {
width: 80%;
}

input {
width: 100%
}

button {
width: 100%;
margin-top: 15px;
margin-left: 0;
}
}

@media only screen and (min-width: 640px) {
.App {
width: 60%;
}

input {
width: 50%;
}

button {
width: 30%;
margin-left: 10px;
margin-top: 0;
}
}
```


Quittez.

Dans le répertoire src, ouvrez le fichier index.css

```
vim index.css
```

Copiez et collez le code ci-dessous :

```
body {
margin: 0;
padding: 0;
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", "Roboto", "Oxygen",
"Ubuntu", "Cantarell", "Fira Sans", "Droid Sans", "Helvetica Neue",
sans-serif;
-webkit-font-smoothing: antialiased;
-moz-osx-font-smoothing: grayscale;
box-sizing: border-box;
background-color: #282c34;
color: #787a80;
}

code {
font-family: source-code-pro, Menlo, Monaco, Consolas, "Courier New",
monospace;
}
```


Allez dans le répertoire Todo

```
cd ../..
```

Lorsque vous êtes dans le répertoire Todo, exécutez :

```
npm run dev
```

En supposant qu'il n'y ait pas d'erreurs lors de l'enregistrement de tous ces fichiers, notre application To-Do devrait être prête et entièrement fonctionnelle avec les fonctionnalités discutées précédemment :
créer une tâche, supprimer une tâche et afficher toutes vos tâches..


![5012](https://user-images.githubusercontent.com/85270361/210132689-3bccdc9b-0dcd-47e9-b1eb-008e05505d47.PNG)


Félicitations !
Dans ce Projet #3, vous avez créé une simple application To-Do et l'avez déployée avec la stack MERN. 
Vous avez écrit une application frontend en utilisant React.js qui communique avec une application backend écrite en Express.js.
Vous avez également créé un backend MongoDB pour stocker les tâches dans une base de données.

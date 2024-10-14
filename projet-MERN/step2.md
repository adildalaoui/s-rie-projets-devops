# INSTALLATION D'EXPRESSJS

Rappelez-vous qu'Express est un framework pour Node.js. Par conséquent, beaucoup de choses que les développeurs auraient dû programmer sont déjà prises en charge par défaut. Cela simplifie le développement et abstrait de nombreux détails de bas niveau. Par exemple, Express aide à définir les routes de votre application en fonction des méthodes HTTP et des URL.

Pour utiliser Express, installez-le en utilisant npm :

```
npm install express
```

Maintenant, créez un fichier index.js avec la commande ci-dessous :

```
touch index.js
```

Exécutez ls pour confirmer que votre fichier index.js a été créé avec succès.

Installez le module dotenv.

```
npm install dotenv
```

Ouvrez le fichier index.js avec la commande ci-dessous :

```
vim index.js
```

Tapez le code ci-dessous et enregistrez. Ne vous laissez pas submerger par le code que vous voyez. Pour l’instant, collez simplement le code dans le fichier.

```
const express = require('express');
require('dotenv').config();

const app = express();

const port = process.env.PORT || 5000;

app.use((req, res, next) => {
res.header("Access-Control-Allow-Origin", "\*");
res.header("Access-Control-Allow-Headers", "Origin, X-Requested-With, Content-Type, Accept");
next();
});

app.use((req, res, next) => {
res.send('Welcome to Express');
});

app.listen(port, () => {
console.log(`Server running on port ${port}`)
});
```


Remarquez que nous avons spécifié d'utiliser le port 5000 dans le code. Cela sera nécessaire plus tard lorsque nous utiliserons le navigateur.

Utilisez :w pour enregistrer dans vim et :qa pour quitter vim.

Il est maintenant temps de démarrer notre serveur pour voir s'il fonctionne. Ouvrez votre terminal dans le même répertoire que votre fichier index.js et tapez :

```
node index.js
```

Si tout se passe bien, vous devriez voir "Server running on port 5000" dans votre terminal.

![5000](https://user-images.githubusercontent.com/85270361/210130555-4322307c-3f48-4ff5-afc2-06a2b389cd94.PNG)



Maintenant, nous devons ouvrir ce port dans les groupes de sécurité EC2. Référez-vous à l'Étape 1 du Projet 1 – Installation du serveur web Nginx. Là, nous avons créé une règle d'entrée pour ouvrir le port TCP 80, vous devez faire de même pour le port 5000, comme ceci :



![5001](https://user-images.githubusercontent.com/85270361/210130592-7d3c477d-c6b7-4682-ad88-577b65fb8444.PNG)


Ouvrez votre navigateur et essayez d'accéder à l'adresse IP publique ou au nom DNS public de votre serveur, suivi du port 5000 :

```
http://<PublicIP-or-PublicDNS>:5000
```


Petit rappel sur la façon d'obtenir l'adresse IP publique et le nom DNS public de votre serveur :

Vous pouvez le trouver dans votre console web AWS dans les détails EC2.
Exécutez curl -s http://169.254.169.254/latest/meta-data/public-ipv4 pour l'adresse IP publique.
Exécutez curl -s http://169.254.169.254/latest/meta-data/public-hostname pour le nom DNS public.



![5002](https://user-images.githubusercontent.com/85270361/210130631-8edbc957-719f-4323-ae55-b9df9614899e.PNG)


Routes
Il y a trois actions que notre application de liste de tâches (To-Do) doit pouvoir effectuer :

Créer une nouvelle tâche
Afficher la liste de toutes les tâches
Supprimer une tâche terminée
Chaque tâche sera associée à un point de terminaison particulier et utilisera différentes méthodes de requête HTTP standard : POST, GET, DELETE.

Pour chaque tâche, nous devons créer des routes qui définiront divers points de terminaison sur lesquels l'application To-Do dépendra. Créons donc un dossier routes.



```
mkdir routes
```


Astuce : Vous pouvez ouvrir plusieurs terminaux dans Putty ou Linux/Mac pour vous connecter à la même instance EC2.

Changez de répertoire pour entrer dans le dossier routes.

```
cd routes
```

Maintenant, créez un fichier api.js avec la commande ci-dessous :

```
touch api.js
```


Ouvrez le fichier avec la commande ci-dessous :

```
vim api.js
```

Copiez le code ci-dessous dans le fichier. (Ne vous laissez pas submerger par le code


```
const express = require ('express');
const router = express.Router();

router.get('/todos', (req, res, next) => {

});

router.post('/todos', (req, res, next) => {

});

router.delete('/todos/:id', (req, res, next) => {

})

module.exports = router;
```


Pour avancer, créons le répertoire Models.

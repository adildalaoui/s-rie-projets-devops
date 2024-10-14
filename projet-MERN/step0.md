# Dans ce projet, vous êtes chargé de mettre en œuvre une solution web basée sur la pile MERN dans le cloud AWS.

## La pile MERN Web se compose des composants suivants :

- MongoDB : Une base de données NoSQL orientée documents, utilisée pour stocker les données de l'application sous forme de documents.
- ExpressJS : Un framework d'application web côté serveur pour Node.js.
- ReactJS : Un framework frontend développé par Facebook. Il est basé sur JavaScript et utilisé pour construire des composants d'interface utilisateur (UI).
- Node.js : Un environnement d'exécution JavaScript. Il est utilisé pour exécuter du JavaScript sur une machine plutôt que dans un navigateur.

![proj3](https://user-images.githubusercontent.com/85270361/210118416-5abdf8d5-5fb8-4caf-b315-3d98d45a9e3d.PNG)


Comme illustré ci-dessus, un utilisateur interagit avec les composants d'interface utilisateur ReactJS situés sur le front-end de l'application dans le navigateur. 
Ce front-end est servi par le back-end de l'application résidant sur un serveur, via ExpressJS qui fonctionne sur NodeJS.

Toute interaction entraînant une demande de modification de données est envoyée au serveur Express basé sur NodeJS, qui récupère les données de la base de données MongoDB si nécessaire, et renvoie les données au front-end de l'application, qui sont ensuite présentées à l'utilisateur.

Auto-apprentissage supplémentaire

Faites des recherches sur les types de systèmes de gestion de bases de données (SGBD) qui existent et pour quels usages chaque type est plus adapté. Soyez capable d'expliquer la différence entre les SGBD relationnels et NoSQL (de différents types).
Familiarisez-vous avec le concept des frameworks d'applications Web. Apprenez quels frameworks côté serveur (backend) et côté client (frontend) existent et à quoi ils servent.
Entraînez-vous à la syntaxe de base de JavaScript pour le plaisir.
Explorez ce qu'est une API RESTful et à quoi elle sert dans le développement Web.
Lisez à quoi servent les feuilles de style en cascade (CSS) et consultez la syntaxe et les propriétés de base.
Instructions pour soumettre votre travail pour examen et retour
Pour soumettre votre travail pour examen et retour – suivez ces instructions.

# Préparation des prérequis
Pour compléter ce projet, vous aurez besoin d'un compte AWS et d'un serveur virtuel avec le système d'exploitation Ubuntu Server.

Si vous n'avez pas de compte AWS – retournez à l'Étape 0 du Projet 1 pour vous inscrire à un compte AWS dans l'offre gratuite et créer une nouvelle instance EC2 de la famille t2.nano avec l'image Ubuntu Server 20.04 LTS (HVM). N'oubliez pas que vous pouvez avoir plusieurs instances EC2, mais assurez-vous d'ARRÊTER celles sur lesquelles vous ne travaillez pas actuellement afin d'économiser les heures gratuites disponibles.

Astuce #1 : Lorsque vous créez vos instances EC2, vous pouvez ajouter une balise "Nom" avec une valeur correspondant au projet actuel sur lequel vous travaillez – cela sera reflété dans le nom de l'instance EC2. Comme ceci :

![pro3](https://user-images.githubusercontent.com/85270361/210118546-bead7609-5dea-4538-86f6-2e69c17408cc.PNG)


# Tâche

Déployer une simple application de liste de tâches (To-Do) qui crée des listes de tâches comme ceci :

![porr3](https://user-images.githubusercontent.com/85270361/210118580-173d44bc-f848-48a3-b63d-4aed7998c638.PNG)

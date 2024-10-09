# STEP 6 – RÉCUPÉRATION DE DONNÉES À PARTIR DE LA BASE DE DONNÉES MYSQL AVEC PHP (SUITE)

Dans cette étape, vous allez créer une base de données (BD) de test avec une simple "Liste de tâches" et configurer l'accès à celle-ci, afin que le site Nginx puisse interroger des données depuis la base de données et les afficher.

Au moment de la rédaction de ce document, la bibliothèque PHP MySQL native mysqlnd ne prend pas en charge caching_sha2_authentication, la méthode d'authentification par défaut pour MySQL 8. Nous devrons créer un nouvel utilisateur avec la méthode d'authentification mysql_native_password pour pouvoir nous connecter à la base de données MySQL depuis PHP.

Nous allons créer une base de données nommée example_database et un utilisateur nommé example_user, mais vous pouvez remplacer ces noms par d'autres valeurs.

Tout d'abord, connectez-vous à la console MySQL en utilisant le compte root :

```
sudo mysql
```

Pour créer une nouvelle base de données, exécutez la commande suivante depuis votre console MySQL :

```
mysql> CREATE DATABASE `example_database`;
```
Maintenant, vous pouvez créer un nouvel utilisateur et lui accorder tous les privilèges sur la base de données que vous venez de créer.

La commande suivante crée un nouvel utilisateur nommé example_user, en utilisant mysql_native_password comme méthode d'authentification par défaut. Nous définissons le mot de passe de cet utilisateur comme étant password, mais vous devriez remplacer cette valeur par un mot de passe sécurisé de votre choix.

```
mysql>  CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'password';
```

Maintenant, nous devons donner à cet utilisateur les permissions sur la base de données example_database :

```
mysql> GRANT ALL ON example_database.* TO 'example_user'@'%';

```
Cela donnera à l'utilisateur example_user tous les privilèges sur la base de données example_database, tout en empêchant cet utilisateur de créer ou de modifier d'autres bases de données sur votre serveur.

Maintenant, quittez le shell MySQL avec :

```
mysql> exit
```

Vous pouvez tester si le nouvel utilisateur a les bonnes permissions en vous reconnectant à la console MySQL, cette fois en utilisant les identifiants de l'utilisateur personnalisé :
```
mysql -u example_user -p
```

Remarquez le drapeau -p dans cette commande, qui vous demandera le mot de passe utilisé lors de la création de l'utilisateur example_user. Après vous être connecté à la console MySQL, confirmez que vous avez accès à la base de données example_database :

```
mysql> SHOW DATABASES;

```

Cela vous donnera la sortie suivante :

```
Output
+--------------------+
| Database           |
+--------------------+
| example_database   |
| information_schema |
+--------------------+
2 rows in set (0.000 sec)
```
Ensuite, nous allons créer une table de test nommée todo_list. Depuis la console MySQL, exécutez la déclaration suivante :

```
CREATE TABLE example_database.todo_list (
mysql>     item_id INT AUTO_INCREMENT,
mysql>     content VARCHAR(255),
mysql>     PRIMARY KEY(item_id)
mysql> );
```

Insérez quelques lignes de contenu dans la table de test. Vous voudrez peut-être répéter la commande suivante plusieurs fois en utilisant différentes valeurs :

```
mysql> INSERT INTO example_database.todo_list (content) VALUES ("My first important item");
```
Pour confirmer que les données ont été correctement enregistrées dans votre table, exécutez :
```
mysql>  SELECT * FROM example_database.todo_list;mysql>  SELECT * FROM example_database.todo_list;
```

Vous verrez la sortie suivante :
```
Output
+---------+--------------------------+
| item_id | content                  |
+---------+--------------------------+
|       1 | My first important item  |
|       2 | My second important item |
|       3 | My third important item  |
|       4 | and this one more thing  |
+---------+--------------------------+
4 rows in set (0.000 sec)
```

Après avoir confirmé que vous avez des données valides dans votre table de test, vous pouvez quitter la console MySQL :

```
mysql> exit
```

Maintenant, vous pouvez créer un script PHP qui se connectera à MySQL et interrogera votre contenu. Créez un nouveau fichier PHP dans votre répertoire racine personnalisé à l'aide de votre éditeur préféré. Nous allons utiliser nano pour cela :
```
nano /var/www/projectLEMP/todo_list.php
```

Le script PHP suivant se connecte à la base de données MySQL et interroge le contenu de la table todo_list, affichant les résultats dans une liste. S'il y a un problème avec la connexion à la base de données, il lancera une exception.

Copiez ce contenu dans votre script todo_list.php :

```
<?php
$user = "example_user";
$password = "password";
$database = "example_database";
$table = "todo_list";

try {
  $db = new PDO("mysql:host=localhost;dbname=$database", $user, $password);
  echo "<h2>TODO</h2><ol>";
  foreach($db->query("SELECT content FROM $table") as $row) {
    echo "<li>" . $row['content'] . "</li>";
  }
  echo "</ol>";
} catch (PDOException $e) {
    print "Error!: " . $e->getMessage() . "<br/>";
    die();
}
```


Enregistrez et fermez le fichier une fois que vous avez terminé vos modifications.

Vous pouvez maintenant accéder à cette page dans votre navigateur web en visitant le nom de domaine ou l'adresse IP publique configurée pour votre site web, suivie de /todo_list.php :

```
http://<Public_domain_or_IP>/todo_list.php
```

Vous devriez voir une page comme celle-ci, affichant le contenu que vous avez inséré dans votre table de test :

![projje2-s](https://user-images.githubusercontent.com/85270361/210118271-529eb3c8-9bc2-4b05-b3c7-7d6553405fb9.PNG)


Cela signifie que votre environnement PHP est prêt à se connecter et à interagir avec votre serveur MySQL.

Félicitations ! Dans ce guide, nous avons construit une base flexible pour servir des sites et des applications PHP à vos visiteurs, en utilisant Nginx comme serveur web et MySQL comme système de gestion de base de données.

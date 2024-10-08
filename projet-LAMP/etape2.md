# STEP 2 — INSTALLATION DE MYSQL

Maintenant que nous avez un serveur web opérationnel, nous devons installer un Système de Gestion de Base de Données (SGBD) pour pouvoir stocker et gérer les données de notre site dans une base de données relationnelle. MySQL est un système de gestion de base de données relationnelle populaire utilisé dans les environnements PHP, donc nous l'utiliserons dans notre projet.

Encore une fois, utilisons `apt` pour acquérir et installer ce logiciel :
```
$ sudo apt install mysql-server
```

Lorsque vous y êtes invité, confirmez l'installation en tapant Y, puis ENTREE
Lorsque l'installation est terminée, connectez-vous à la console MySQL en tapant :

```
$ sudo mysql
```

Cela vous connectera au serveur MySQL en tant qu'utilisateur administratif de la base de données root, ce qui est sous-entendu par l'utilisation de sudo lors de l'exécution de cette commande. Vous devriez voir une sortie comme celle-ci :


```
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 11
Server version: 8.0.22-0ubuntu0.20.04.3 (Ubuntu)

Copyright (c) 2000, 2020, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> 
```

Quittez le shell MySQL avec :

```
mysql> exit
```




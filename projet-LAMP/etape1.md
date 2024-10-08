# ÉTAPE 1 — INSTALLATION D'APACHE 

### Qu'est-ce qu'Apache exactement ?

Apache HTTP Server est le logiciel de serveur web le plus utilisé au monde. Développé et maintenu par la Fondation Apache, Apache est un logiciel open-source disponible gratuitement. Il fonctionne sur 67 % de tous les serveurs web dans le monde. Il est rapide, fiable et sécurisé. Il peut être largement personnalisé pour répondre aux besoins de nombreux environnements différents grâce à l'utilisation d'extensions et de modules.

La plupart des fournisseurs d'hébergement WordPress utilisent Apache comme logiciel de serveur web. Cependant, les sites web et autres applications peuvent fonctionner sur d'autres logiciels de serveur web tels que Nginx, Microsoft IIS, etc.

Le serveur web Apache est parmi les serveurs les plus populaires au monde. Il est bien documenté, dispose d'une communauté active d'utilisateurs et a été largement utilisé pendant une grande partie de l'histoire du web, ce qui en fait un excellent choix par défaut pour l'hébergement de sites web.

### Installation d'Apache avec le gestionnaire de paquets d'Ubuntu ‘apt’ :

```bash
# Mettre à jour la liste des paquets dans le gestionnaire de paquets
sudo apt update

# Installer le paquet apache2
sudo apt install apache2
```

### Vérifier qu'Apache fonctionne

Pour vérifier qu'Apache fonctionne comme un service sur notre système d'exploitation, utilisez la commande suivante :

```bash
sudo systemctl status apache2
```
### Ouvrir le port entrant 80

Notre serveur fonctionne et nous pouvons y accéder localement et depuis Internet ("ip:80").

Tout d'abord, vérifions comment y accéder localement dans notre shell Ubuntu, exécutez :

```bash
curl http://localhost:80
```
### Tester l'accès depuis Internet

Il est temps pour nous de tester comment notre serveur HTTP Apache peut répondre aux requêtes depuis Internet. 


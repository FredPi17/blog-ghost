Blog Ghost
==========

Ce projet est un déploiement de la solution de site internet Ghost

Préparation du projet
-----------

1. Cloner le projet:

    git clone https://github.com/FredPi17/blog-ghost

Puis aller dans le dossier :

    cd blog-ghost

2. Créer le fichier `digitalocean.ini` dans `.secrets/certbot/` en vous basant sur `digitalocean.ini.example`. Remplacer alors la valeur de `dns_digitalocean_token` pour votre clé d'API préalablement générée dans votre compte [ici](https://cloud.digitalocean.com/account/api/tokens). 

3. Installer le plugin dns-digitalocean de certbot comme ceci : 

    apt install python3-certbot-dns-digitalocean

4. Puis générez les clés de chiffrement de votre site : 

    certbot certonly \
    --dns-digitalocean \
    --dns-digitalocean-credentials .secrets/certbot/digitalocean.ini \
    -d example.com

Déploiement
-----------

Maintenant que le projet est pret, il ne reste plus qu'à le déployer. 

Pour cela, il faut s'assurer que vous avez docker-compose. Si ce n'est pas le cas, l'installer comme ceci : 

    apt install docker docker-compose -y 

Puis déployer le projet : 

    docker-compose up -d

Erreurs connues
---------------

Il peut arriver que la base de donnéer mysql ne soit pas terminée d'être déployée quand Ghost veut s'y connecter. Cela a pour conséquence que Ghost ne démarre pas. Pour remédier à cela, il faut re-exécuter la commande : 

    docker-compose up -d 

Travaux futurs
--------------

- Créer volume pour mysql pour faire persister les données sur le serveur hote
- Ajouter fichier de variables d'environement pour : nom de domaine, variable de déploiement letsencrypt, etc.. 
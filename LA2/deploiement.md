## Sommaire

- [Sommaire](#sommaire)
- [Prérequis](#prérequis)
- [Déployer le projet](#déployer-le-projet)

Il existe 2 méthodes pour déployer le projet septotrip en règle générale.

## Prérequis

- Processeur x86
- 1 Go de RAM minimum
- Docker et Docker-compose
- Connexion internet

## Déployer le projet

1. Se connecter sur la machine où héberger Septotrip
2. Cloner le projet [septotrip-compose](https://github.com/La-Sectoblique/septotrip-compose) et accéder au dossier ainsi créé
3. Créer un dossier `letsencrypt` pour stocker les certificats HTTPS
4. Dupliquer le fichier `.env.example` et renommer le fichier `.env`
5. Remplir le fichier `.env` ainsi :
```properties
# Général

# l'url de base du service 
# c'est cette propriété qui va définir avec quelle URL seront disponibles les différents services 
URL=septotrip.com

# clé pour la génération des tokens api
# à remplir avec une longue chaine de caractères aléatoires
JWT_SECRET_KEY=treslonguechainequivaservirdebasepourcreerdestokensjwt

# adresse email de la personne délivrant le certificat HTTPS
HOST_EMAIL=user@example.com


# Minio

# nom d'utilisateur pour l'utilisateur root de minio
MINIO_ROOT_USER=root

# mot de passe de l'utilisateur route
MINIO_ROOT_PASSWORD=P@l1l@dM1n

# chemin vers le dossier ou seront stockés les fichiers contenus dans minio
MINIO_PATH=/chemin/vers/le/dossier


# Database

# nom de la base de données
DB_NAME=septotrip

# nom de l'utilisateur de base
DB_USER=palila

# mot de passe de l'utilisateur de base
DB_PASSWORD=D0i0ur3M3mbeur
```
Ici, le fichier est rempli avec des valeurs d'exemple.

6. Lancer la commande suivante
```bash
(sudo) docker-compose -f ./docker-compose.prod.yml --env-file .env up -d
```
Une fois que la commande a rendu la main, les différents services sont disponibles à ces URL : 
- Webapp : `https://<l'URL donné dans le docker compose>`
- API : `https://api.<l'URL donné dans le docker compose>`
- Documentation du package NPM : `https://doc.<l'URL donné dans le docker compose>`
- Console Minio : `https://stash.<l'URL donné dans le docker compose>`
- Postgres : sur l'adresse du serveur sur le port 5432 pour la base de données de production, et sur le port 5433 pour la base de données de test




# Documentation développeur de l'API

## Sommaire

- [Documentation développeur de l'API](#documentation-développeur-de-lapi)
  - [Sommaire](#sommaire)
  - [Installation d'un environnement de développement](#installation-dun-environnement-de-développement)
    - [Prérequis](#prérequis)
    - [Installation d'une base de données et d'un service de stockage en local](#installation-dune-base-de-donnée-et-dun-service-de-stockage-en-local)
    - [Clonage du dépôt Github et installation des dépendances](#clonage-du-dépôt-github-et-installation-des-dépendances)
    - [Configuration de l'API](#configuration-de-lapi)
  - [Structure et organisation du code](#structure-et-organisation-du-code)
  - [Ajouter de nouveaux éléments à l'API](#ajouter-de-nouveaux-éléments-à-lapi)

## Installation d'un environnement de développement

### Prérequis

- Node.js 16
- Docker (recommandé)

### Installation d'une base de données et d'un service de stockage en local

*Dans cette partie, nous allons voir l'installation de ces éléments avec Docker, mais il est également possible d'installer directement PostGres et Minio en local directement, ou d'utiliser un serveur externe avec un service S3 et PostGres d'accessible.*  

Afin de pouvoir développer sur l'API, nous allons commencer par installer les éléments indispensables au fonctionnement de celle ci.  
Pour cela, assurez vous que le service Docker est lancé. Pour s'en assurer : 
- Sur Linux, tapez la commande suivante : 
```
systemctl is-active docker
```
Si la commande affiche `active` alors Docker est bien lancé. Sinon, revérifiez votre installation de Docker.
- Sur Windows, ouvrez l'application `Docker Desktop` et vérifiez que le logo Docker en bas à gauche indique `ENGINE RUNNING`, sinon revérifiez votre installation de Docker.

![API_Docker_windows_launched](img/API_Docker_windows_launched.png)

Maintenant que Docker est lancé, ouvrez un terminal et tapez les commandes suivantes : 
```bash
# Sur linux, il se peut qu'il faille executer ces commandes en tant que root
docker run -p 5432:5432 --name septodb-dev -e POSTGRES_DB=septoblique-dev -e POSTGRES_USER=api -e POSTGRES_PASSWORD=aaa -d postgis/postgis

docker run -p 9000:9000 -p 9001:9001 -e MINIO_ROOT_USER=api -e MINIO_ROOT_PASSWORD=password -e MINIO_BROWSER_REDIRECT_URL=http://stash.localhost minio/minio server /data --console-address ":9001"
```

Si aucune erreur n'est renvoyée, vous avez alors une base de données et un service de stockage S3 disponible en local.

### Clonage du dépôt Github et installation des dépendances

Pour importer tout le projet, ouvrez un terminal et tapez les commandes suivantes : 
```bash
# Si cette commande ne fonctionne pas, connectez vous à github avec git
git clone git@github.com:La-Sectoblique/septotrip-api.git
cd septotrip-api
# Pour importer les types
git submodule init
git submodule update
```

Une fois le projet cloné et complet, installez `yarn` si ce n'est pas déjà fait avec la commande `npm install --global yarn`.   
Installez ensuite les dépendances du projet avec la commande `yarn install`.

Une fois l'installation terminée, tapez la commande `yarn build` pour être sûr que tout est installé correctement. 

### Configuration de l'API

Une fois le repo cloné et les dépendances installées, nous allons configurer l'API pour qu'elle fonctionne dans un environnement de développement.  
Pour cela, clonez le fichier `.env.example` et renommez le en `.env`, puis, remplissez le ainsi : 

```properties
# GLOBAL
NODE_ENV=development
API_PORT=3000
# POSTGRES
POSTGRES_HOST=localhost
POSTGRES_DB=septoblique-dev
POSTGRES_USER=api
POSTGRES_PASSWORD=aaa
POSTGRES_PORT=5432
# SECURITY
JWT_SECRET_KEY=unechainedecaracterestreslonguepourlagenerationdetokenjwt
# S3
S3_ACCESS_KEY_ID=api
S3_SECRET_ACCESS_KEY=password
S3_ENDPOINT=localhost
```

Si vous avez configuré Minio ou Postgres différement, remplissez le `.env` avec les informations correspondantes.

Pour être sur que l'api est correctement paramétrée, tapez la commande `yarn dev` pour la lancer avec `nodemon`.

Si l'API se lance, tout est correctement installé !

## Structure et organisation du code

Le code de l'API est structuré ainsi : 

![API_code_structure](img/API_code_structure.png)

L'essentiel du code de l'API se trouve dans le dossier `src`. Celui est structuré de cette manière : 

- controllers

Ce dossier contient tous les contrôleurs qui détiennent l'essentiel de l'intelligence de l'API. Chaque fichier contient les contrôleurs d'un item précis (exemple: `Trip.ts` contient les contrôleurs des voyages).

- core

Ce dossier contient tous les éléments de base de l'api, comme les fonctions de connexion à la base de données, par exemple.

- middlewares
  - loaders

Le dossier `middlewares` contient toutes les fonctions qui sont appelées avant les contrôleurs lors d'un appel sur une route. Le dossier `loaders` contient tous les middlewares qui vont chercher en base une entité en base de données avant que le contrôleur ne la manipule.

- models

Ce dossier contient tous les modèles de la base de données ainsi que leurs relations entre eux.

- routes
  - protected
  - public

Le dossier `routes` contient toutes les routes exposées par l'API. Le dossier `protected` contient toutes les routes accessibles uniquement en étant connecté à un compte utilisateur, tandis que le dossier `public` contient toutes les routes accessibles sans être connecté.

- types
  - errors
  - models
  - utils

Le dossier `types` contient toutes les déclarations de types. 
Le dossier `errors` contient les déclarations d'erreurs, le dossier `models` les déclarations de modèles et le dossier `utils` d'autres types importants.

- utils

Ce dossier contient plusieurs fonctions généralistes.

## Ajouter de nouveaux éléments à l'API


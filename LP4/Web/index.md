# Documentation développeur de l'application web

## Sommaire
- [Documentation développeur de la WebApp](#documentation-développeur-de-la-webapp)
	- [Sommaire](#sommaire)
	- [Installation d'un environnement de développement](#installation-dun-environnement-de-développement)
		- [Prérequis](#prérequis)
		- [Clonage du dépôt Github](#clonage-du-dépôt-github)
		- [Installation des dépendances](#installation-des-dépendances)
		- [Configuration de l'environnement de l'application](#configuration-de-lenvironnement-de-lapplication)
            - [Connexion avec l'api](#connexion-avec-lapi)
            - [Création du token mapbox](#création-du-token-mapbox)
        - [Extensions VsCode recommandée](#extensions-VsCode-recommandée)
        - [Lancement de l'application](#lancement-de-lapplication)
	- [Structure et organisation du code](#structure-et-organisation-du-code)
        - [Modules](#modules)
        - [Store](#store)
	
## Installation d'un environnement de développement

### Prérequis

- Node.js 16
- Accès à mapbox

### Clonage du dépôt Github

Pour commencer, il est nécessaire de cloner le projet

```bash
git clone git@github.com:La-Sectoblique/septotrip-webapp.git
```

### Installation des dépendances

L'une des dépendance de l'application est le septotrip-sevice, qui est utilisé par nos applications front-end pour effectuer tout les appels vers l'API.

Pour configurer les droits d'installation de ce package il vous faut :

- Générer un [personnal access token github](https://github.com/settings/tokens/new) avec les droits `read:packages`
- Copier coller le fichier `.npmrc.example` à la racine du projet en `.npmrc`
- Rentrer le token générer dans le fichier en suivant cet exemple (token fictif)

    ```
    //npm.pkg.github.com/:_authToken=ghp_PDFhdfsqdjqdsfqfs987fsq64prout
    @la-sectoblique:registry=https://npm.pkg.github.com
    ```

Une fois cet étape effectuée, installez `yarn` si ce n'est pas déjà fait avec la commande `npm install --global yarn`.   
Installez ensuite les dépendances du projet avec la commande `yarn` ou `yarn install`.

### Configuration de l'environnement de l'application

#### Connexion avec l'api

L'application passe par les variables d'environnements d'angular situé dans `/src/environments`

- Copier coller le fichier `environment.template.ts` en `environment.ts`
- Modifier l'url vers l'api (dans le cas du septotrip originel: `baseURL: 'https://api.septotrip.com'`)

#### Création du token mapbox

Pour gérer la carte, Septotrip utilise mapbox. Pour ce faire il est nécessaire de créer un compte.
Cette dépendance peut être assez contraignante. Une migration vers [mapLibre](https://github.com/maplibre/ngx-maplibre-gl) est cependant certainement possible.

- Créer un compte [mapbox](https://account.mapbox.com/auth/signup/)
- Récuperer le token
- L'ajouter dans `environment.ts`: `mapBoxToken: 'pk.fdsqmifsqpodufhdsqmfsqfoshqfdsdf684sqdf6'`

### Extensions VsCode recommandée

- [Angular Files](https://marketplace.visualstudio.com/items?itemName=alexiv.vscode-angular2-files)
- [Angular Language Service](https://marketplace.visualstudio.com/items?itemName=Angular.ng-template)
- [Auto Rename Tag](https://marketplace.visualstudio.com/items?itemName=formulahendry.auto-rename-tag)
- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)

### Lancement de l'application

Pour lancer l'application et vérifier que tout fonctionne, vous n'aurez plus qu'à faire :
```
yarn start
```

Si tout ce passe bien, l'application devrait être disponible sur `localhost:4200`

## Structure et organisation du code

Dans cette documentation, nous prendrons pour aquis les bases d'Angular.
Pour les néophytes, le tutoriel d'introduction au framework est disponible [ici](https://angular.io/tutorial).

L'entièreté du code de l'application est située dans le dossier `/src`.

Il est composé de plusieurs sous dossiers:
- app : Ensemble des fichiers de l'application (composants, page, services, store, etc...)
- assets : Différents élements graphiques ou visuel de l'application (font, traductions, animations lottie, images)
- environments : Variables d'environement, comme vu tout à l'heure
- style : Fichiers de style globaux de l'application (variables, utils, etc...)

Nous allons détailler plus en détail la structure du dossier `app` qui est la plus intéressante à voir.

### Modules

Le dossier module est découper en deux sous dossier: Core & Feature

Core contient les élements principaux de l'application.
Feature contient tout ce qui est en rapport avec les fonctionnalités métier de l'application

*note: Certains modules ne sont pas placés au bon endroit, comme authentication qui est dans feature :)*

Nous allons détailler la structure classique d'un module :

- Un fichier `[feature-name].module.ts`
- Un dossier `components` contenant les différents composants de la feature
- Un dossier `services` conteant les service de la feature. C'est là que sont appelés les fonctions du service septotrip. Les fonctions du service sont wrappés dans ces services pour respecter le plus possible les conventions d'Angular (si il n'y avait pas de service, on aurait fait nos appels http ici directement). Cela permet de centraliser ce qui doit être modifié si on arrête d'utiliser le service ou qu'il subit des modification. Tout le reste de la logique de l'application ne sera pas impacté par de tel changements.
- Un dossier `models` qui contient les différentes interfaces ou enumeration nécessaire au bon fonctionnement de la feature.
- Un dossier `pages`. Il n'est pas toujours présent. J'ai décider de faire une distinction entre les pages et les composants (bien qu'il s'agisse de la même chose). Pour distinguer les deux le plus facilement possible: Une page ne devrait jamais être appelée dans un composant.

### Store

L'application implémente un patterne REDUX pour le traitement et le stockage des données de navigation de l'utilisateur.

La libraire [NgRx](https://ngrx.io/) est donc utilisée.

Le Store de l'application est découpé en plusieurs parties: Trip, map, files. 

La partie Trip pourrait faire l'objet de simplification et d'un redécoupage car elle regroupe toutes les fonctionnalités (Steps, Points, Path etc...)

L'utilisation de cette librairie permet de n'avoir qu'une seule source de vérité pour toutes les informations de l'application ce qui permet une belle stabilité dans la gestion de ces dernières.
# Documentation développeur de l'API

## Sommaire
- [Documentation développeur de la WebApp](#documentation-développeur-de-la-webapp)
	- [Sommaire](#sommaire)
	- [Installation d'un environnement de développement](#installation-dun-environnement-de-développement)
		- [Prérequis](#prérequis)
		- [Clonage du dépôt Github](#clonage-du-dépôt-github)
		- [Installation des dépendances](#installation-des-dépendances)
        - [Extensions VsCode recommandée](#extensions-VsCode-recommandée)
        - [Lancement de l'application](#lancement-de-lapplication)
	- [Structure et organisation du code](#structure-et-organisation-du-code)
        - [Modules](#modules)
        - [Store](#store)


## Installation d'un environnement de développement

### Prérequis

- Node.js 16
- Git
- Compte google developer
- Un compte expo
- L'application Expo Go

### Clonage du dépôt Github

Pour importer tout le projet, ouvrez un terminal et tapez les commandes suivantes : 
```bash
# Si cette commande ne fonctionne pas, connectez vous à github avec git
git@github.com:La-Sectoblique/septotrip-mobile.git
cd septotrip-mobile
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

### Extensions VsCode recommandée

- [ESLint](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint)
### Lancement de l'application

Pour lancer l'application et vérifier que tout fonctionne, vous n'aurez plus qu'à faire :
```
expo start
```
Puis ouvrir dans le même réseau Wifi privée que votre ordinateur l'application `Expo Go` sur votre smartphone est scanné le QR code.

## Structure et organisation du code

Le code de l'API est structuré ainsi : 

![Mobile_code_structure](img/structure.png)

L'essentiel du code de l'API se trouve dans le dossier `src`. Celui est structuré de cette manière : 

- pages

Ce dossier contient tous les pages principales liés au route défini dans nos navigations (présente dans `models/NavigationParamList.ts`).

- components

Ce dossier contient tous les composants créer pour l'application, rangé par objet provenant de l'API lié.

- navigation

Le dossier `navigation` contient les navigations imbriquées à celle principale situé dans le `App.tsx`.

- models

Ce dossier contient tous les types customs que vous pourriez avoir à créer durant le développement.

- app.json

Ceci est le dossier de config de l'application, il contiendra vos clés d'API, les permissions nécessaires au lancement de votre application etc..



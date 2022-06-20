## Sommaire

- [Sommaire](#sommaire)
- [Descriptif des applications](#descriptif-des-applications)
  - [1. Application web](#1-application-web)
  - [2. Application mobile](#2-application-mobile)
  - [3. API](#3-api)
  - [4. Service NPM](#4-service-npm)

## Descriptif des applications

Le projet Septotrip est divisé en 3 applications : une application web, une application mobile et une API. 
Nous avons fait le choix d'écrire ces briques en `TypeScript`, afin d'avoir une cohérence entre les applications et de pouvoir réutiliser du code entre ces applications. Les différentes fonctions réutilisables pour les applications web et mobile sont réunies dans le package npm `septoblique-service`.

### 1. Application web

L'application web de Septotrip est l'application permettant de plannifier ses voyages en amont de celui ci.
Cette application utilise le framework `Angular`, car c'est le framework web avec lequel nous sommes le plus familier.

### 2. Application mobile

L'application mobile de Septotrip est l'application qui va accompagner l'utilisateur au cours de son voyage. 
Cette application utilise la librairie `React native`, afin de pouvoir faire l'application en `TypeScript` et de garder une cohérence avec les autres applications du projet, mais également car cette librairie nous permet d'avoir une base de code commune pour Android et iOS.
De plus, beaucoup de librairies tierces sont disponible pour `React native`, ce qui facilite grandement le développement d'application complexe.

### 3. API

L'API est l'application qui fait le lien entre les différents clients et qui contient le modèle de données.
Elle utilise les libraires `express` pour les routes d'API et `sequelize` pour les communications avec la base de données. Nous avons choisi `express` car cette librairie apporte une grande flexibilité dans la gestion des routes et des middlewares. Quand à `sequelize`, nous l'avons utilisé comme ORM car c'est une librairie très utilisé dans l'écosystème JavaScript, et fonctionne bien avec `TypeScript` et la structure de l'API.
Egalement, afin de faciliter le développement et éviter le code dupliqué, nous avons mis toutes les déclarations de type des modèles dans [un submodule git](https://github.com/La-Sectoblique/septotrip-types) utilisé par le service et l'API.

### 4. Service NPM

Le service NPM Septotrip est un package NPM contenant tout les appels à l'API. 
Nous avons utilisé pour cette partie, la librairie `axios` afin de faciliter l'envoi de requête HTTP vers l'API. L'avantage de cette librairie est qu'elle est compatible avec `react native` et avec `angular`.
Ce package partage aussi le submodule git de déclaration de git, afin que les clients puisse également avoir accès a ces types.   
Une documentation du service est disponible [ici](https://doc.septotrip.com).
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

L'application web de Septotrip est l'application permettant de planifier ses voyages en amont de celui ci.
Cette application utilise le framework `Angular`, car c'est le framework web qui nous est le plus familier.

l'application web de Septotrip permet de planifier ses voyages.
Elle utilise le framework `Angular`. Il permet un développement stable de part la structure que prend l'application. Il est également le plus connus de nos développeurs front.
L'application est écrit avec `Typescript` ce qui permet une bien meilleure stabilité. 
Tout les appels API passent par le service `septoblique-service`, ce qui lui permet de ne pas avoir à s'occuper de la gestion http des appels directement.
Toutes les données de l'utilisateur tel que les voyages ou les étapes sont gérés avec `NgRx`, une librairie implémentant le pattern Redux, permettant de gérer un état global pour l'application.
La carte est géré avec Mapbox. Cette librairie de carte permet une grande rapiditée de développement car elle très complète et assez simple d'utilisation.

### 2. Application mobile

L'application mobile de Septotrip est l'application qui va accompagner l'utilisateur au cours de son voyage. 
Cette application utilise la librairie `React native`, en `TypeScript`. L'utilisation de `TypeScript` permet de garder une cohérence avec les autres applications du projet. La librairie `React native` nous permet également d'avoir une base de code commune pour les appareils Android et iOS.
De plus, beaucoup de librairies tierces sont disponibles conjointement à `React native`, afin de faciliter grandement le développement de fonctionnalités complexes.

### 3. API

L'API est l'application qui fait le lien entre les différents clients et qui contient le modèle de données.
Elle utilise les libraires `express` pour les routes d'API et `sequelize` pour les communications avec la base de données. Nous avons choisi `express` car cette librairie apporte une grande flexibilité dans la gestion des routes et des middlewares. Quand à `sequelize`, nous l'avons utilisé comme ORM car c'est une librairie très utilisée dans l'écosystème JavaScript, et fonctionne bien avec `TypeScript` et la structure de l'API.
Egalement, afin de faciliter le développement et éviter le code dupliqué, nous avons mis toutes les déclarations de type des modèles dans [un submodule git](https://github.com/La-Sectoblique/septotrip-types) utilisé par le service et l'API.

### 4. Service NPM

Le service NPM Septotrip est un package NPM contenant tous les appels à l'API. 
Nous avons utilisé pour cette partie, la librairie `axios` afin de faciliter l'envoi de requêtes HTTP vers l'API. L'avantage de cette librairie est qu'elle est compatible avec `react native` et avec `angular`.
Ce package partage aussi le submodule git de déclaration de git, afin que les clients puissent également avoir accès a ces types.   
Une documentation du service est disponible [ici](https://doc.septotrip.com).

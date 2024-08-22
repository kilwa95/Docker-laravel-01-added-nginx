# Laravel Docker Project

Ce projet est une configuration Docker pour un environnement Laravel, comprenant des services pour Nginx, PHP, MySQL, Composer, Artisan, et NPM.

## Prérequis

- [Docker](https://www.docker.com/get-started) doit être installé sur votre machine.
- [Docker Compose](https://docs.docker.com/compose/install/) doit être installé.

## Structure des dossiers

- src/ : Ce répertoire contiendra le code source de votre application Laravel.
- dockerfiles/ : Ce répertoire contient les Dockerfiles personnalisés pour les différents services.

## Services Docker

La configuration Docker comprend les services suivants :

- server : Un conteneur Nginx servant de serveur web.
    Port exposé : 8000 (correspondant au port 80 à l'intérieur du conteneur)
    Dépendances : php, mysql
    php : Un conteneur PHP, utilisé pour exécuter l'application Laravel.

- mysql : Un conteneur MySQL 5.7 pour la base de données.
    Fichier d'environnement : ./env/mysql.env

- composer : Un conteneur pour Composer, utilisé pour gérer les dépendances PHP.
    Volume monté : ./src (monté sur /var/www/html dans le conteneur)

- artisan : Un conteneur pour exécuter les commandes Artisan de Laravel.
    Volume monté : ./src (monté sur /var/www/html dans le conteneur)
  
- Entrypoint : php /var/www/html/artisan

- npm : Un conteneur Node.js utilisé pour gérer les dépendances JavaScript via NPM.
    Version Node.js : 14
    Volume monté : ./src (monté sur /var/www/html dans le conteneur)
    Entrypoint : npm

## Utilisation

### Cloner le dépôt

```bash
git clone https://votre-repo.git
cd votre-repo
```
### Construire et démarrer les conteneurs

```bash
docker-compose up --build
```
### Exécuter des commandes Artisan

```bash
docker-compose run --rm artisan migrate
```
### Gérer les dépendances avec Composer

```bash
docker-compose run --rm composer install
```
### Gérer les dépendances JavaScript avec NPM

```bash
docker-compose run --rm npm install
```
### Arrêter les conteneurs

```bash
docker-compose down
```
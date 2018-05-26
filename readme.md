# IMPORTANT
Le dépôt officielle, source pour Classroom est dans : https://github.com/frederic-baucher/EXU9231 (c'est un dépôt natif, pas un fork, dans lequel on peut faire des recherche avec la barre de recherche github !)
Le [présent dépôt](https://github.com/fbab/quickstart-basic) est destiné aux tests pour préparer un beau EXU9231 !

# BILAN
 - branche V4 : la connection à la BD est enfin opérationnelle
   - correction la plus pertinente : cp .env.travis .env (.env.testing n'est pas pris en charge par travis)


# DOCUMENTATION
## Introduction
Testé avec PHP 7.0 en local.
Le numéro de version de Laravel est dans composer.lock (ligne 310) :
 - "name": "laravel/framework",
 - "version": "v5.2.20",

## Installation en local

    navigateur> http://localhost/phpmyadmin
      créer une base de données FILR4LARAVEL

    console> cd /tmp
    
    console> git clone https://github.com/laravel/quickstart-basic quickstart

    console> cd quickstart
    
    console> cp .env.local .env
    
    console> vi .env
       indiquer le mot de passe de la base sur la variable d'environnement DB_PASSWORD
       
    console> composer install

    console> php artisan migrate

    console> php artisan serve
    
    navigateur> http://localhost:8000/

[Complete Tutorial](https://laravel.com/docs/5.2/quickstart)


# Installation en distant - HEROKU

## Les principales difficultés pour déployer du Laravel sous HEROKU
 - Toutes les opérations ne peuvent être faite en ligne sur https://dashboard.heroku.com/apps/, l'usage d'un client heroku-cli installé en local est quelquefois indispensable :(
 - HEROKU ne voit pas les variables d'environnement déclarées dans .env
   - Les variables d'environnement doivent être déclarées
     - soit sur le portail https://dashboard.heroku.com/apps/filrouge2quickstart/settings
     - soit via la ligne de commande : heroku config:set DATABASE_URL=postgres://username:password@machine:5432/database
 - HEROKU supporte nativement Postgres et le paramétrage passe NECESSAIREMENT par la variable d'environnement DATABASE_URL
 - les opérations d'initialisation ne peuvent être scriptée et doivent exécutées
   - soit via la console du portail https://dashboard.heroku.com/apps/filrouge2quickstart/settings
   - soit via la ligne de commande : heroku run php artisan migrate:refresh --env=testing --no-interaction -vvv --app filrouge2quickstart


Liste de commandes (qui peuvent être jouées dans la console en ligne)
 - php artisan migrate:install --env=testing --no-interaction -vvv
 - php artisan migrate:refresh --env=testing --no-interaction -vvv

Liste de commandes (à jouer dans une console en local)
 - heroku run php artisan migrate:install --env=testing --no-interaction -vvv --app filrouge2quickstart 
 - heroku run php artisan migrate:refresh --env=testing --no-interaction -vvv --app filrouge2quickstart 
 - heroku config:set APP_ENV=development APP_DEBUG=true APP_LOG_LEVEL=debug
 - heroku config:set APP_KEY=b809vCwvtawRbsG0BmP1tWgnlXQypSKf
 - heroku config:set APP_LOG=errorlog

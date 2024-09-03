# MySecondSymfonyC1

Installation de la version lts (Long Term Support) avec la majorité des bibliothèques pour un site wep (`--webapp`)

    symfony new MySecondSymfonyC1 -- webapp --version=lts

## Mise à jour des versions de sécurités

    composer update

## Lancement du serveur

    symfony serve -d
    ou
    symfony server:start -d

Pour le fermer

    symfony server:stop

L'adresse est généralement de type https://127.0.0.1:8000/

### Création d'un contrôleur

    symfony console make:controller
    ou
    php bin/console make:controller

Le nom doit être en PascalCase terminé par Controller, mais Symfony se charge de le corriger en cas d'oubli.

    php bin/console make:controller Home
    created: src/Controller/HomeController.php
    created: templates/home/index.html.twig

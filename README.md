# MySecondSymfonyC1

Installation de la version lts (Long Term Support) avec la majorité des bibliothèques pour un site wep (`--webapp`)

    symfony new MySecondSymfonyC1 -- webapp --version=lts

en cas d'oubli de --webapp

    cd MySecondSymfonyC1
    composer require webapp

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

On va vérifier la route par défaut

    php bin/console debug:route

#### Modification de la route

```php
    src/Controller/HomeController.php

# ...

    #[Route('/home', name: 'homepage')]
    public function index(): Response

# ...

```

On peut accéder à l'accueil depuis la racine de notre

https://127.0.0.1:8000/

#### Modification de base.html.twig

```twig
{# templates/base.html.twig"}
{# ... #}
<title>{% block title %}MySecondSymfonyC1{% endblock %}</title>
" ...

```

#### Modification de index.html.twig

```twig

{# template/index.html.twig #}
{# ... #}
{#{% block title %}{{ parent() }} | {{ title }}{% endblock %}#}
{# ... #}
  <div class="container">
        <h1>{{ title }}</h1>
        <nav>
            {# on utilise path('nom du chemin') lorsqu'on veut un lien vers une page#}
            <a href="{{ path('Homepage) }}">Homepage</a>
        </nav>
    </div>

```

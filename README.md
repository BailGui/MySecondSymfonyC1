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

#### Création du menu avec twig

templates/home/menu.html.twig

```twig

<nav>
    {# on utilise path('nom du chemin') lorsqu'on veut un lien vers une page#}
    <a href="{{ path('homepage') }}">Homepage</a>
    <a href="{{ path('about_me') }}">About me</a>
</nav>

```

#### Modification de index.html.twig

```
{% extends 'base.html.twig' %}

{# on surcharge le block title avec {{ parent }}
    et le titre passé par le contrôleur
#}
{% block title %}{{ parent() }} | {{ title }}{% endblock %}


{% block body %}
    <div class="container">
        <h1>{{ title }}</h1>
{# inclusion depuis la racine du projet ! (templates) #}
{% include 'home/menu.html.twig' %}
    </div>

{% endblock %}`
```

About est similaire.

#### Création de notre .env.local

Le fichier .env est le fichier de configuration qui est mis sur git et donc github

C'est pour celà que nous allons le copier sous le nom de .env.local

```
cp .env .env.local
```

Ouvrez .env.local

Changez cette ligne

```
APP_ENV=dev
APP_SECRET=c6f06c078199d1f00879e1b9c146cddf
en

APP_ENV=prod
APP_SECRET=une_autre_clef_secrete_sécurité
```

si vous retapez php bin/console debug:route

Vous ne trouverez plus que les routes de production

Dans le fichier .env.local

### Trouvez la ligne de base de données :

```

# DATABASE_URL="mysql://app:!ChangeMe!@127.0.0.1:3306/app?serverVersion=8.0.32&charset=utf8mb4"

# DATABASE_URL="mysql://app:!ChangeMe!@127.0.0.1:3306/app?serverVersion=10.11.2-MariaDB&charset=utf8mb4"

DATABASE_URL="postgresql://app:!ChangeMe!@127.0.0.1:5432/app?serverVersion=16&charset=utf8"
Commentez la ligne postgresql et décommentez la ligne mysql

Ensuite passez vos paramètres de connexion dans l'ordre

utilisateur:mot_de_passe@ip_serveur:port/nomdelaDB?options

DATABASE_URL="mysql://root:@127.0.0.1:3306/mysecondesymfonyc1?serverVersion=8.0.31&charset=utf8mb4"

# DATABASE_URL="mysql://app:!ChangeMe!@127.0.0.1:3306/app?serverVersion=10.11.2-MariaDB&charset=utf8mb4"

# DATABASE_URL="postgresql://app:!ChangeMe!@127.0.0.1:5432/app?serverVersion=16&charset=utf8"

```

### Création de la DB

```
php bin/console doctrine:database:create

```

La base de donnée devrait être créée si mysql.exe est activé ou Wamp démarré

### Création d'une entité

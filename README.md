# movielibrary

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, check out the [documentation](https://nuxtjs.org).

## Special Directories

You can create the following extra directories, some of which have special behaviors. Only `pages` is required; you can delete them if you don't want to use their functionality.

### `assets`

The assets directory contains your uncompiled assets such as Stylus or Sass files, images, or fonts.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/assets).

### `components`

The components directory contains your Vue.js components. Components make up the different parts of your page and can be reused and imported into your pages, layouts and even other components.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/components).

### `layouts`

Layouts are a great help when you want to change the look and feel of your Nuxt app, whether you want to include a sidebar or have distinct layouts for mobile and desktop.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/layouts).

### `pages`

This directory contains your application views and routes. Nuxt will read all the `*.vue` files inside this directory and setup Vue Router automatically.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/get-started/routing).

### `plugins`

The plugins directory contains JavaScript plugins that you want to run before instantiating the root Vue.js Application. This is the place to add Vue plugins and to inject functions or constants. Every time you need to use `Vue.use()`, you should create a file in `plugins/` and add its path to plugins in `nuxt.config.js`.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/plugins).

### `static`

This directory contains your static files. Each file inside this directory is mapped to `/`.

Example: `/static/robots.txt` is mapped as `/robots.txt`.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/static).

### `store`

This directory contains your Vuex store files. Creating a file in this directory automatically activates Vuex.

More information about the usage of this directory in [the documentation](https://nuxtjs.org/docs/2.x/directory-structure/store).

### Next features

Pousser les composants encore plus loin pour créer une véritable bibliothèque (buttons, texts, cards, ...).
Stores.
Utiliser les variables SCSS pour y définir les couleurs de TMDB.
Transferer les paramètres bases d'API (URL et token) dans un fichier .env.
Design plus poussé et affiné.
Barre de recherche dans la barre de navigation pour une page de résultats plus légère.
Ajouter la possibilité de lister les films par catégories via une barre de tags au dessous de la barre de recherche (design semblable aux propositions de catégories personnalisées sur YouTube).
Prise en charge plus vaste des retours d'erreurs.
Aller plus loin pour la page de détails pour un film (rectification de l'erreur au chargement, ajout d'une bande annonce).
Passer la note des films qui est actuellement /10 à une note /5 afin d'alleger le rating avec étoiles.
Barre de recherche plus poussée avec la possibilité d'ajouter ou supprimer des filtres.

### Ultra features

Compte utilisateur avec profil.
Système de favori pour les films, qui se retrouveront regroupés dans une liste propre à l'utilisateur.
Possibilité d'échanger des recommandations de films entre les users.
Ajouter des paramètres de navigation (light mode / dark mode, langue du contenu).

## Moved to GitLab

**Warning**: This project has been moved to GitLab: https://gitlab.com/balping/asset-bundler

----

# Asset Bundler for Laravel Modules

This package provides a command that generates a `js` and an `scss` file that bundles all assets provided by each of your modules.

## Install

```
composer require --dev balping/asset-bundler
```

This package is auto-discovered by Laravel, there's no need to register the provider manually.

## Usage

Modules should include `index.js` and `index.scss` files. Example file structure:

```
project-root/
  ├── Modules/
    ├── MyModule/
      ├── Resources/
        ├── assets/
          ├── js/
            ├── index.js
          ├── sass/
            ├── index.scss
      ├── npm
        ├── package.json
```

Running

```
php artisan module:bundle-assets
```

generates `modules.js` and `modules.scss` files in your main assets directory that you can require in `app.js` and import in `app.scss`:

```js
require('./modules');
```

```scss
@import "modules";
```

Your module can have node dependencies too. If there's a `package.json` in the root of a module, asset bundler creates the file `resources/installed-modules/package.json` that requires your module's `package.json` as a dependency. So if you add the following to your main `package.json` file, all node dependencies of your modules will be required.

```json
{
    "private": true,
    "scripts": {
        // ...
    },
    "devDependencies": {
        // ...
        "installed-modules": "file:resources/installed-modules"
    }
}
```

## License

This library is licensed under GPLv3.

# Laravel Breeze - Nuxt.js Edition

## Introduction

This repository is an implementation of the [Laravel Breeze](https://laravel.com/docs/starter-kits) application / authentication starter kit frontend in [Nuxt.js](https://nuxtjs.org). All of the authentication boilerplate is already written for you - powered by [Laravel Sanctum](https://laravel.com/docs/sanctum), allowing you to quickly begin pairing your beautiful Nuxt.js frontend with a powerful Laravel backend.

## Official Documentation

### Installation

First, create a Nuxt.js compatible Laravel backend by installing Laravel Breeze into a [fresh Laravel application](https://laravel.com/docs/installation) and installing Breeze's API scaffolding:

```bash
# Create the Laravel application...
laravel new nuxt-backend

cd nuxt-backend

# Install Breeze and dependencies...
composer require laravel/breeze

php artisan breeze:install api

# Make sure you've updated your database connection in your .env file and run...
php artisan migrate

# Serve the application...
php artisan serve
```

Next, clone this repository and install its dependencies with `yarn install` or `npm install`. Then, open nuxt.config.js file and supply the URL of your backend:

```js
env: {
    backendUrl: 'http://localhost:8000'
},
...
axios: {
    baseURL: 'http://localhost:8000'
},
...
auth: {
    strategies: {
        laravelSanctum: {
            url: 'http://localhost:8000'
        },
    }
}
```

Finally, run the application via `npm run dev` / `yarn dev`. The application will be available at `http://localhost:3000`:

```
npm run dev
```
or
```
yarn dev
```

> Note: Currently, we recommend using `localhost` during local development of your backend and frontend to avoid CORS "Same-Origin" issues.

## Inspiration
This project was inspired by the [Breeze Nuxt.js](https://github.com/laravel/breeze-next) project. Have fun!

## License

Laravel Breeze Nuxt is open-sourced software licensed under the [MIT license](LICENSE.md).

# Social network demo website with laravel and vuejs
Use php artisan passport:keys if needed

## Steps taken to configure this project:

> laravel new social
- create database
> php artisan migrate

> composer require laravel/passport

> composer require intervention/image // resizes images

> php artisan migrate

> php artisan passport:install
- in config/auth.php add this to guards array elements: 'api' => ['driver' => 'passport','provider' => 'users','hash' => false]
- in Kernel.php add this middleware to web group: \Laravel\Passport\Http\Middleware\CreateFreshApiToken::class
- in Users.php: add use HasApiTokens;
> composer require laravel/ui

> php artisan ui vue

> php artisan ui:auth

> npm install

> php artisan make:controller AppController

> npm install vue-router --save-dev

> yarn install

> yarn add dropzone //for image upload

> npm run watch

Ide helper:
> composer require --dev barryvdh/laravel-ide-helper
>
> php artisan ide-helper:generate


Note: use composer on linux and yarn install, npm run watch on windows

To create a model and migration:
> php artisan make:model ModelX -m

Interesting relationship:
```
public function coverImage(): HasOne
{
    return $this->hasOne(UserImage::class)
        ->orderByDesc('id')
        ->where('location', 'cover');
}
```

[![Build Status](https://travis-ci.org/Algo-Web/POData-Laravel.svg?branch=master)](https://travis-ci.org/Algo-Web/POData-Laravel)
[![Scrutinizer Code Quality](https://scrutinizer-ci.com/g/Algo-Web/POData-Laravel/badges/quality-score.png?b=master)](https://scrutinizer-ci.com/g/Algo-Web/POData-Laravel/?branch=master)
[![Coverage Status](https://coveralls.io/repos/github/Algo-Web/POData-Laravel/badge.svg?branch=master)](https://coveralls.io/github/Algo-Web/POData-Laravel?branch=master)
[![Latest Stable Version](https://poser.pugx.org/algo-web/podata-laravel/v/stable)](https://packagist.org/packages/algo-web/podata-laravel)
[![Latest Unstable Version](https://poser.pugx.org/algo-web/podata-laravel/v/unstable)](https://packagist.org/packages/algo-web/podata-laravel)
[![Total Downloads](https://poser.pugx.org/algo-web/podata-laravel/downloads)](https://packagist.org/packages/algo-web/podata-laravel)
[![Monthly Downloads](https://poser.pugx.org/algo-web/podata-laravel/d/monthly)](https://packagist.org/packages/algo-web/podata-laravel)
[![Daily Downloads](https://poser.pugx.org/algo-web/podata-laravel/d/daily)](https://packagist.org/packages/algo-web/podata-laravel)

# POData-Laravel
Composer Package to provide Odata functionality to Laravel.

With support for Laravel 5.7 since PostgreSQL support in Laravel 5.1 is broken.

To install, run
```
composer require algo-web/podata-laravel
```

Edit `config/app.php` and add this to providers section:

```php
AlgoWeb\PODataLaravel\Providers\MetadataProvider::class,
AlgoWeb\PODataLaravel\Providers\MetadataRouteProvider::class,
AlgoWeb\PODataLaravel\Providers\QueryProvider::class,
AlgoWeb\PODataLaravel\Providers\MetadataControllerProvider::class,
Illuminate\Notifications\NotificationServiceProvider::class,
```

You then add the trait to the models you want to expose.

```php
    use \AlgoWeb\PODataLaravel\Models\MetadataTrait;
```

By default, following Laravel convention, POData-Laravel pluralises the
model names to use as endpoints.
That's an implementation choice in POData-Laravel, not anything intrinsic to OData itself.

Eg, for User model, all else equal:
```php
    /odata.svc/Users
```

If you have just installed the package and have trouble reaching your models'
endpoints, try setting APP_DISABLE_AUTH=true in your project's .env file
temporarily, and then try reaching those endpoints again.

-- Known Limitations --

* Cannot expose two models with the same class name in different
namespaces - trying to expose both App\Foo\Model and App\Bar\Model
will trip an exception complaining that resource set has already been
added.
* This can be worked around by setting a custom endpoint name on one
of the colliding models.
* Controller input parameters map 'id' to underlying model's primary key

-- Configuration options --
These need to go in your Laravel project's .env file.

* APP_METADATA_CACHING - Whether or not to turn model metadata caching on
* APP_METADATA_CACHE_DURATION - If caching, how long (in minutes) to
retain cached metadata
* APP_DISABLE_AUTH - Disable authentication (boolean)
* APP_DRY_RUN - Roll back DB changes unconditionally (boolean)

## Contributing

See CONTRIBUTING.md for the details.


## Features Supported

(thanks to @renanwilliam for the initial version of this list)

* [ ] Full CRUD Support
* [x] $count
* [x] $filter
  * [x] Comparison Operators
    * [x] eq
    * [x] ne
    * [x] lt
    * [x] le
    * [x] gt
    * [x] ge
  * [x] Logical Operators
    * [x] and
    * [x] or
    * [x] not
  * [x] Comparison Operators
    * [x] has
  * [x] String Functions
    * [x] indexof
    * [x] contains
    * [x] endswith
    * [x] startswith
    * [x] length
    * [x] substring
    * [x] tolower
    * [x] toupper
    * [x] trim
    * [x] concat
  * [x] Arithmetic Operators
    * [x] add
    * [x] sub
    * [x] mul
    * [x] div
    * [x] mod
  * [x] Date Functions
    * [x] year
    * [x] month
    * [x] day
    * [x] hour
    * [x] minute
    * [x] second
    * [x] fractionalseconds
    * [x] date
    * [x] time
    * [x] totaloffsetminutes
    * [x] now
    * [x] mindatetime
    * [x] maxdatetime
  * [x] Math Functions
    * [x] round
    * [x] floor
    * [x] ceiling
* [x] $select
* [x] $top
* [x] $skip
* [x] $skiptoken
* [x] $orderby
* [x] $expand

The capabilities under $filter currently rely on the deprecated-in-PHP-7.2
create_function capability.

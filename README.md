# DriftPHP - Mysql adapter


This is a simple adapter for Mysql on top of ReactPHP and DriftPHP. Following
the same structure that is followed in the Symfony ecosystem, you can use this
package as a Bundle, only usable under DriftPHP Framework.

## Install

You can install the package by using composer

```bash
composer require manuelacosta98/mysql-bundle:dev-master
```

## Configure

This package will allow you to configure all your Mysql async clients, taking
care of duplicity and the loop integration. Once your package is required by
composer, add the bundle in the kernel and change your `services.yaml`
configuration file to defined the clients

```yaml
mysql:
    clients:
        users:
            host: "localhost"
            port: 3306
            database: "/users"
            username: "root"
            password: "secret"
        
        orders:
            database: "/orders"
```

Only host is required. All the other values are optional.

## Use it

Once you have your clients created, you can inject them in your services by
using the name of the client in your dependency injection arguments array

```yaml
a_service:
    class: My\Service
    arguments:
        - "@mysql.users_client"
        - "@mysql.orders_client"
```

You can use Autowiring as well in the bundle, by using the name of the client
and using it as a named parameter

```php
public function __construct(
    Client $usersClient,
    Client $ordersClient
)
```
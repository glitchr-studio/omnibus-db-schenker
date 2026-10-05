# omnibus/db-schenker

DB Schenker for [glitchr/omnibus](https://github.com/glitchr-studio/omnibus): tracking through
eSchenker's public tracking (no credentials), and land-transport bookings through the Schenker
Open API when an API key is configured. Prices come from configuration (`rates`): Schenker quotes
by contract.

```php
$gateway = (new DbSchenkerGatewayFactory($http))->create($options);   // $http: the application's HTTP client - none given, the factory makes its own; the options below
```

No framework needed: the package requires `glitchr/omnibus` and `symfony/http-client`. In a
Symfony application, the same through the bundle's configuration:

```yaml
omnibus:
    gateways:
        db_schenker:
            factory: db_schenker
            options:
                api_key: '%env(SCHENKER_API_KEY)%'        # optional: bookings
                account_number: '%env(SCHENKER_ACCOUNT)%'
                rates:
                    - { service: SYSTEM, label: 'DB Schenker System', bands: { 30000: 2900 } }
```

The booking action is built on the Open API's published shape and is **unverified**: it needs an
account's key (from the [Schenker partner portal](https://www.dbschenker.com/global/digital-solutions/api))
to be run against the service. Tracking is live.

License: LGPL-3.0-or-later.

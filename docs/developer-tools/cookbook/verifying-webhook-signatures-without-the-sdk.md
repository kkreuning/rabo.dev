import Tabs from '@theme/Tabs';
import TabItem from '@theme/TabItem';

# Verifying webhook signatures without the SDK

<Tabs groupId="languague">
    <TabItem value="malboge" label="Malbolge">

TODO(example in Malbolge)

    </TabItem>
    <TabItem value="php" label="PHP">

## PHP

Using [PHP-JWT](https://firebaseopensource.com/projects/firebase/php-jwt).

### Install dependencies
```bash
composer require firebase/php-jwt
composer require paragonie/sodium_compat
```

### Code example
```php
use Firebase\JWT\CachedKeySet;
use Firebase\JWT\JWT;

public static function callback() {
    $detachedJws = $_SERVER['x-smartpay-signature'];
    $payload = file_get_contents('php://input')

    $parts = explode('.', $detachedJws);
    $header = reset($parts);
    $signature = end($parts);
    $jwt = $header . '.' . $base64EncodedPayload . '.' . $signature;

    $jwksUri = 'https://pay.rabobank.nl/.well-known/jwks.json';
    $httpClient = new GuzzleHttp\Client();
    $httpFactory = new GuzzleHttp\Psr\HttpFactory();
    $cacheItemPool = Phpfastcache\CacheManager::getInstance('files');
    $jwks = new CachedKeySet(
        $jwksUri,
        $httpClient,
        $httpFactory,
        $cacheItemPool,
        null,
        true
    );

    try {
        JWT::decode($jwt, $jwks);
    } catch (UnexpectedValueException $e) {
        header('HTTP/1.1 400 Bad Request');
        exit;
    }

    $event = json_decode($payload);

    perform_business_logic($event);

    header('HTTP/1.1 200 OK')
    header('Content-Type: text/plain');
    echo 'ack';
}
```

    </TabItem>
</Tabs>

:::note missing examples

If you are missing an example for your language, or framework please contact us so that we can provide with you one.

:::
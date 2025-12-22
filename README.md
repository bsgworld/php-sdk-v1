# BSG PHP SDK (V1 - Legacy API)

Official PHP SDK for BSG API - SMS, Viber, HLR/MNP messaging services.

> **Note:** This is the legacy V1 API. For new projects, consider using [bsg/php-sdk](https://packagist.org/packages/bsg/php-sdk) (V2 One-API).

## Installation

```bash
composer require bsg/php-sdk-v1
```

## Requirements

- PHP 7.4 or later
- Guzzle HTTP client

## Quick Start

```php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use BSG\Api\V1\Configuration;
use BSG\Api\V1\Api\SMSApi;

// Configure API key
$config = Configuration::getDefaultConfiguration()
    ->setApiKey('X-API-KEY', 'YOUR_API_KEY');

// Create API instance
$smsApi = new SMSApi(new GuzzleHttp\Client(), $config);

// Send SMS
try {
    $result = $smsApi->smsCreateObjects([
        'destination' => 'phone',
        'originator' => 'YourSender',
        'body' => 'Hello from BSG!',
        'msisdn' => ['380501234567']
    ]);
    print_r($result);
} catch (Exception $e) {
    echo 'Error: ' . $e->getMessage();
}
```

## Available APIs

| API | Description |
|-----|-------------|
| `SMSApi` | Send SMS messages, check delivery status, get pricing |
| `ViberApi` | Send Viber messages |
| `HLRApi` | HLR (Home Location Register) lookups |
| `MNPApi` | MNP (Mobile Number Portability) lookups |
| `CommonApi` | Account balance, tariffs |
| `ExportsApi` | Data export operations |

## Examples

### Check Balance

```php
$commonApi = new BSG\Api\V1\Api\CommonApi(new GuzzleHttp\Client(), $config);
$balance = $commonApi->commonGetBalanceBase();
echo "Balance: " . $balance->getBalance();
```

### Send Viber Message

```php
$viberApi = new BSG\Api\V1\Api\ViberApi(new GuzzleHttp\Client(), $config);
$result = $viberApi->viberCreateObjects([
    'originator' => 'YourViberSender',
    'body' => 'Hello via Viber!',
    'msisdn' => ['380501234567']
]);
```

### HLR Lookup

```php
$hlrApi = new BSG\Api\V1\Api\HLRApi(new GuzzleHttp\Client(), $config);
$result = $hlrApi->hlrCreateObjects([
    'msisdn' => ['380501234567']
]);
```

## API Documentation

- [SMS API](docs/Api/SMSApi.md)
- [Viber API](docs/Api/ViberApi.md)
- [HLR API](docs/Api/HLRApi.md)
- [MNP API](docs/Api/MNPApi.md)
- [Common API](docs/Api/CommonApi.md)

## Configuration

### API Host

Default: `https://api.bsg.world`

```php
$config = Configuration::getDefaultConfiguration()
    ->setHost('https://api.bsg.world')
    ->setApiKey('X-API-KEY', 'YOUR_API_KEY');
```

### Timeout

```php
$client = new GuzzleHttp\Client([
    'timeout' => 30,
    'connect_timeout' => 10
]);
$smsApi = new SMSApi($client, $config);
```

## Support

- Website: [bsg.world](https://bsg.world)
- Email: support@bsg.world
- Documentation: [bsg.world/developers](https://bsg.world/developers)

## License

MIT
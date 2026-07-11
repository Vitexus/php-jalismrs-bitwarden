# php-jalismrs-bitwarden

Debian package for [jalismrs/bitwarden-php](https://github.com/jalismrs/bitwarden-service.php) — a PHP library providing services to access Bitwarden vault data via the Bitwarden CLI.

## Requirements

- PHP >= 8.0
- `symfony/process` ^6.0
- [Bitwarden CLI](https://bitwarden.com/help/article/cli/) (`bw`) must be installed on the host system

If necessary, set a custom bitwarden server url:

```bash
bw config server <SERVER_URL>
```

## Installation

### Via Debian package

```bash
sudo apt install php-jalismrs-bitwarden
```

Files are installed to `/usr/share/php/Jalismrs/Bitwarden/`.

### Via Composer

```bash
composer require jalismrs/bitwarden-php
```

## Usage

You must implement the `BitwardenServiceDelegate` interface to provide credentials and session management:

```php
use Jalismrs\Bitwarden\BitwardenService;
use Jalismrs\Bitwarden\BitwardenServiceDelegate;
use Jalismrs\Bitwarden\Model\BitwardenItem;

$service = new BitwardenService(new MyBitwardenDelegate());
$items = $service->searchItems('web5902');

/** @var BitwardenItem $item */
$item = $items[0];
var_dump($item->getId());
var_dump($item->getName());
var_dump($item->getLogin()?->getUsername());
var_dump($item->getLogin()?->getPassword());
```

## Building the Debian package

```bash
dpkg-buildpackage -us -uc -b
```

## Testing

```bash
composer install
vendor/bin/phpunit
```

## Upstream

- **Source**: https://github.com/jalismrs/bitwarden-service.php
- **Packagist**: https://packagist.org/packages/jalismrs/bitwarden-php
- **Version**: 1.1.0

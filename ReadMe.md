# FreeGeoIp for PHP
> **FreeGeoIp for PHP** is a simple library used to interface with a freegeoip API.

> **Hint**: FreeGeoIp for PHP is available through [Composer](https://getcomposer.org). `composer require nafisc/freegeoip-php`.

[![StyleCI](https://styleci.io/repos/115560334/shield?style=flat)](https://styleci.io/repos/115560334)
[![Latest Stable Version](https://poser.pugx.org/nafisc/freegeoip-php/v/stable?format=flat)](https://packagist.org/packages/nafisc/freegeoip-php)
[![Total Downloads](https://poser.pugx.org/nafisc/freegeoip-php/downloads?format=flat)](https://packagist.org/packages/nafisc/freegeoip-php)
[![Latest Unstable Version](https://poser.pugx.org/nafisc/freegeoip-php/v/unstable?format=flat)](https://packagist.org/packages/nafisc/freegeoip-php)
[![License](https://poser.pugx.org/nafisc/freegeoip-php/license?format=flat)](https://packagist.org/packages/nafisc/freegeoip-php)

### Features
* Retrieve the Geo Location data for any IP address.
* Link to a custom freegeoip server

### Example Usage

#### Include the `FreeGeoIp` class in your code.
```php
use FreeGeoIp\PHP\FreeGeoIp;
```

#### Create the FreeGeoIp object

This will default to `freegeoip.net`.
```php
$freeGeoIp = new FreeGeoIp();
```

Alternately, you can pass it a custom server configuration if you are using the freegeoip binary.
```php
// Address, Port, Protocol, Timeout
$freeGeoIp = new FreeGeoIp(
    'freegeoip.net', 80,
    'http', 10
);
```

#### Lookup a location for an IP Address
```php
// Lookup a location for an IP Address
// and catch any exceptions that might
// be thrown by Guzzle or FreeGeoIP.
try {
    // Retrieve the location information for 
    // github.com by using it's hostname.
    // 
    // This function will work with hostnames
    // or IP addresses.
    $location = $freeGeoIp->getLocationFor('github.com');

    // You can alternately look up the information
    // for the current client's IP address.
    $location = $freeGeoIp->getClientLocation();

    // If we are unable to retrieve the location information
    // for an IP address, null will be returned.
    if ($location == null) {
        echo 'Failed to find location.'.PHP_EOL;
    } else {
        // Convert the location to a standard PHP array.
        print_r($location->_asStdArray());

        // Any of these formats will work for 
        // retrieving a property.
        //
        // See \FreeGeoIp\PHP\Location for a
        // list of available properties.
        echo $location->latitude . PHP_EOL;
        echo $location['longitude'] . PHP_EOL;
        echo $location->region_name() . PHP_EOL;
    }
} catch (\Exception $e) {
    echo $e->getMessage();
}
```
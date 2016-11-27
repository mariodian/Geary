# Geary
Mycelium Gear PHP API - Access all API features of https://gear.mycelium.com.

## Create new Gateway 
In order to use Mycelium Gear API you need to get a gateway ID and secrety. Create new gateway [here](https://admin.gear.mycelium.com/gateways/new).

## Examples

### Create order
````
<?php
require_once('./Geary.php');

$gateway_id = 'XXXXXXXXX';
$gateway_secret = 'YYYYYYYYY';

$price = 13.9;
$keychain_id = 0;

$geary = new Geary($gateway_id, $gateway_secret);
$geary->create_order($price, $keychain_id);
?>
````

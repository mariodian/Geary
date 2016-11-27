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
$order = $geary->create_order($price, $keychain_id);

if ($order->payment_id) {
  // Redirect to a payment gateway
  redirect("https://gateway.gear.mycelium.com/pay/{$order->payment_id}");
}
?>
````

### Cancel order
````
<?php
require_once('./Geary.php');

$gateway_id = 'XXXXXXXXX';
$gateway_secret = 'YYYYYYYYY';

$payment_id = 'XXXXXYYYYY';

$geary = new Geary($gateway_id, $gateway_secret);
$geary->$geary->cancel_order($payment_id);
?>
````

### Check order
````
<?php
require_once('./Geary.php');

$gateway_id = 'XXXXXXXXX';
$gateway_secret = 'YYYYYYYYY';

$payment_id = 'XXXXXYYYYY';

$geary = new Geary($gateway_id, $gateway_secret);
$order = $geary->$geary->check_order($payment_id);

if ($order->payment_id) {
    $url = "https://gateway.gear.mycelium.com/pay/{$order->payment_id}";
    
    // Show a payment gateway URL
    echo '<a href="' . $url . '" target="_blank">Pay</a>';
}
?>
````

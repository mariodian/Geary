# Geary - Mycelium Gear PHP API
Access all API features of https://gear.mycelium.com. 

Create a bitcoin payment gateway for your eshop. Create custom orders with Mycelium Gear Gateway.

![Mycelium Gear Payment Gateway](http://i.imgur.com/a79MjSo.png)

## Create new Gateway 
In order to use Mycelium Gear API you need to get a gateway ID and secret. Create new gateway [here](https://admin.gear.mycelium.com/gateways/new). 

Don't forget to save your gateway secret somewhere safe!

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

### Manualy Check order status
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

### Check order status from Gear's webhook
````
<?php
require_once('./Geary.php');

$gateway_id = 'XXXXXXXXX';
$gateway_secret = 'YYYYYYYYY';

$geary = new Geary($gateway_id, $gateway_secret);
$order = $geary->receive_order();

// Order status was received
if ($order !== FALSE) {
    // Update the local order data
}
?>
````

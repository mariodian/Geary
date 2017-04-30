# Geary - Mycelium Gear PHP API
Access all API features of https://gear.mycelium.com. API documentation is available at https://admin.gear.mycelium.com/docs

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
$geary->cancel_order($payment_id);
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
$order = $geary->check_order($payment_id);

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
$order = $geary->check_order_callback();

// Order status was received
if ($order !== FALSE) {
    // Update the local order data received
    // Data in $order are as follows
    /*
    Array
    (
        [order_id] => 1
        [amount] => 100
        [amount_in_btc] => 0.14628625
        [amount_paid_in_btc] => 0.14628625
        [status] => 2
        [address] => 1NXRQdyb1aTn4ucEGqVDZvFkG9FRyhLWGY
        [transaction_ids] => ["txidXXX"]
        [keychain_id] => 0
        [last_keychain_id] => 0
        [after_payment_redirect_to] => http://example.com/payments/success
        [auto_redirect] => true
        [callback_data] => some random data
    )
    */
} else {
    echo 'Signature mismatch';
}
?>
````

## Support me
Bitcoin donations are welcome at [1x1UnfVJu7cprs3E2jjQ9WRcdDi5KJxAU](https://blockchain.info/address/1x1UnfVJu7cprs3E2jjQ9WRcdDi5KJxAU). Thank you!

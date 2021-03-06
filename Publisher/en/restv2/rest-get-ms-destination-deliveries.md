# REST API: GET destination deliveries (Marketing Suite)

Each emailing is tracked, which allows Copernica to provide you with 
emailing statistics. Deliveries are one of these statistics. You can 
retrieve all deliveries for a specific destination by sending an HTTP GET call to the following URL:

`https://api.copernica.com/v2/ms/destination/{$destinationID}/deliveries?access_token=xxxx`

This method also support the use of the [fields parameter](./rest-fields-parameter) 
for the **timestamp** field.

## Returned fields

The method returns a JSON object with several deliveries. For each delivery 
the following information is available:

* **ID**: The ID of the delivery.         
* **mailing**: The ID of the mailing.
* **timestamp**: The timestamp of delivery.
* **attempts**: Number of attempts made before the delivery.
* **destination**: The ID of the destination that was delivered to.
* **profile**: The ID of the profile that was delivered to.
* **subprofile**: The ID of the subprofile that was delivered to.

## PHP example

This script demonstrates how to use this API method:

```php
// dependencies
require_once('copernica_rest_api.php');

// change this into your access token
$api = new CopernicaRestAPI("your-access-token", 2);

// execute the call
print_r($api->get("ms/destination/{$destinationID}/deliveries"));
```

This example requires the [REST API class](./rest-php).

## More information

* [Overview of all REST API calls](./rest-api)
* [Get all deliveries](./rest-get-ms-deliveries)
* [Get destination abuses](./rest-get-ms-destination-abuses)
* [Get destination clicks](./rest-get-ms-destination-clicks)
* [Get destination errors](./rest-get-ms-destination-errors)
* [Get destination impressions](./rest-get-ms-destination-impressions)
* [Get destination unsubscribes](./rest-get-ms-destination-unsubscribes)

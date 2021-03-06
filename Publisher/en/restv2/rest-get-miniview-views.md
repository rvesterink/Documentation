# REST API: GET database views

To request which selections rely on a miniselection, do an HTTP GET 
request to the following URL:

`https://api.copernica.com/v2/miniview/$id/views?access_token=xxxx`

In this, `$id` needs to be replaced by the numerical identifier or the 
name of the miniview you wish to request the selections for.

## Available parameters

The following parameters can be added to the URL as variables:

- **start**: the first interest to be requested
- **limit**: length of the batch that is requested
- **total**: whether or not the total amount of interests should be counted

More information on the meaning of these parameters can be found [in the article on paging](./rest-paging.md).

## Returned fields

For every selection, the following properties are returned:

- **ID**: the numerical identifier of the selection
- **name**: the name of the selection
- **description**: optional description of the selection
- **parent-type**: used to display whether a selection is placed 
directly under a database, or nested under another selection
- **parent-id**: ID of the parent selection/database
- **has-children**: boolean value: whether or not the database has 
selections nested underneath it
- **has-referred**: boolean value: whether or not there are other 
selections that refer to this selection.
- **has-rules**: boolean value: whether or not the selection has 
selection rules
- **database**: ID of the database this selection belongs to.
- **lastbuilt**: timestamp of the last time the view was built

## PHP example

The following PHP script demonstrates how to use the API method:

```php
// dependencies
require_once('copernica_rest_api.php');

// change this into your access token
$api = new CopernicaRestAPI("your-access-token", 2);

// parameters to pass to the call
$parameters = array(
    'limit'     =>  100
);

// do the call, and print result
print_r($api->get("miniview/{$miniviewID}/views", $parameters));
```

The example above requires the [CopernicaRestApi class](rest-php).

## More information

- [Overview of all API methods](rest-api)
- [GET miniview](./rest-get-miniview)
- [GET miniview rules](./rest-get-miniview-rules)

# REST API: GET database collections

Je kunt collecties van een database opvragen middels een HTTP GET 
request:

`https://api.copernica.com/v2/database/$id/collections?access_token=xxxx`

De `$id` moet je vervangen door de numerieke identifier of de naam van 
de database waar je de collecties van wilt opvragen.

## Beschikbare parameters

De volgende parameters kunnen aan de URL als variabelen worden toegevoegd:

* start: 		eerste collectie die wordt opgevraagd;
* limit: 		lengte van de batch die wordt opgevraagd;
* total: 		toon wel/niet het totaal aantal beschikbare collecties.

Meer informatie over de betekenis van deze parameters vind je in het
[artikel over paging](rest-paging).

## Geretourneerde velden

De methode retourneert een lijst van collecties in de database. Voor elke collectie
worden de volgende eigenschappen teruggegeven:

* id: 			numerieke identifier van de collectie;
* name: 		naam van de collectie;
* database: 	numerieke identifier van de database waartoe de collectie behoort;
* fields: 		array van velden binnen de collectie.

## Voorbeeld in PHP

Het volgende PHP script demonstreert hoe je de API methode kunt aanroepen:

```php
// vereiste scripts
require_once('copernica_rest_api.php');

// verander dit naar je access token
$api = new CopernicaRestAPI("your-access-token", 2);

// parameters voor de methode
$parameters = array(
    'limit'     =>  100
);

// voer de methode uit en print het resultaat
print_r($api->get("database/{$databaseID}/collections", $parameters));
```

Dit voorbeeld vereist de [REST API klasse](rest-php).
    
## Meer informatie

* [Overzicht van alle API calls](rest-api)
* [POST database collections](rest-post-database-collections)
* [GET collection fields](rest-get-collection-fields)
* [POST collection fields](rest-post-collection-fields)

# REST API: GET view

Een methode om de metadata van een database op te vragen. De methode kan 
aangeroepen worden met een HTTP GET verzoek aan de volgende URL:

`https://api.copernica.com/v2/view/$id?access_token=xxxx`

Hier moet de `$id` vervangen worden met de numerieke identifier van de 
database waarvan de selecties moeten worden opgevraagd.

## Beschikbare parameters

Er zijn geen beschikbare parameters voor deze methode.

## Geretourneerde velden

- **id**: unieke numerieke identifier van selectie
- **name**: naam van de selectie
- **description**: beschrijving van de selectie
- **parent-type**: type van de parent (view/database)
- **parent-id**: id van de parent
- **has-children**: geeft aan of de selectie zelf selecties bevat
- **has-referred**: geeft aan of er andere selecties zijn die naar deze selectie refereren.
- **has-rules**: geeft aan of de selectie regels heeft
- **database**: id van de database waar deze selectie onder valt
- **last-built**: tijdstip laatste opbouw van de selectie

## Voorbeeld in PHP

Het volgende voorbeeld demonstreert hoe deze methode gebruikt kan worden met de API:

```php
// vereiste scripts
require_once('copernica_rest_api.php');

// verander dit naar je access token
$api = new CopernicaRestAPI("your-access-token", 2);

// voer de methode uit en print het resultaat
print_r($api->get("view/{$viewID}"));
```

Dit voorbeeld vereist de [REST API klasse](rest-php).

## Meer informatie

* [Overzicht van alle REST API methods](./rest-api)
* [Vraag selectie regels op](./rest-get-view-rules)

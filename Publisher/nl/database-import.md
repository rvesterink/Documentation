# Importeren van profielgegevens
Er zijn verschillende manieren om nieuwe gegevens in te voeren of te importeren.
Zo kun je profielen niet alleen met de hand toevoegen, maar kun je ze ook
aanmaken of bewerken met de API, of importeren vanuit een CSV- of TSV-bestand
(dit zijn bestanden die je onder meer in spreadsheetprogramma's kunt maken).

Het importeren van CSV- of TSV-bestanden is krachtig en kan ook worden gebruikt
voor gelaagde databases met collecties en subprofielen. Ook kun je periodieke
imports maken die automatisch worden herhaald.

## Importbestand voorbereiden
Het bestand dat je wilt importeren moet aan een specifiek formaat voldoen.
Het moet een tab- of kommagescheiden bestand zijn, waarvan de bovenste regel
de kolommen (de veldnamen) bevat die je gaat importeren. Het bestand moet een
UTF-8 encoding hebben en wij raden het aan om quotes om veldwaardes te plaatsen.
Hieronder geven we een voorbeeld van hoe dit bestand eruit kan zien.

    Voornaam,Achternaam,Stad,Telefoonnummer
    'Jan','de Jong','Amersfoort','0612456631'
    'Roos','Schippers','Groningen','0612222444'

Deze bestanden kunnen in bijna alle spreadsheetprogramma's gegenereerd worden.

## Kolommen koppelen
Nadat je een bestand hebt geüpload, moet je de kolommen koppelen. Als het
systeem overeenkomstige namen vindt, zullen die kolommen en velden automatisch
gekoppeld worden. De overige kolommen kun je handmatig koppelen. Meestal
spreekt deze koppeling voor zich: het veld "Voornaam" in het importbestand
koppel je aan het veld "Voornaam" in de database. Als het benodigde veld nog
niet aanwezig is in de database, kun je die ter plekke laten aanmaken.

Je kunt tijdens het koppelen van de kolommen ook *sleutelvelden* instellen.
Sleutelvelden zijn de velden die Copernica gebruikt om regels uit je
importbestand te koppelen aan profielen in de database wanneer je een
profiel updatet. Als er geen match is, kun je instellen dat er een nieuw
profiel moet worden aangemaakt.

## Subprofielen importeren
Je kunt ook imports in gelaagde databases (databases met subprofielen) doen.
In de header van het bestand geef je met een punt als scheidingsteken aan dat
een kolom voor subprofielen wordt gebruikt. Als je een dierenwinkel hebt met
een database met klanten en bij elke klant een collectie van huisdieren, dan
zou je het volgende bestand kunnen uploaden:

    Voornaam,Achternaam,Stad,Dieren.Naam,Dieren.Type
    'Jan','Bakker','Apeldoorn','Blacky','Hond'
    'Jan','Bakker','Apeldoorn','Minoes','Kat'

Zoals je ziet wordt "Jan Bakker" twee keer genoemd. Dit moet je doen, omdat
Jan twee huisdieren heeft en elk huisdier (elke subprofiel dus) op een aparte
regel moet staan. De profieldata ("Jan Bakker") wordt herhaald om aan te geven
dat de twee dieren bij hetzelfde profiel horen. Let wel op dat je goed de
sleutelvelden instelt (ook als je alleen maar nieuwe profielen wilt toevoegen),
omdat Copernica anders niet herkent dat de twee "Jan Bakker"-regels bij elkaar
horen.

## Periodieke imports
Je kunt de importmodule ook gebruiken voor periodieke imports. Je moet dan
geen bestand uploaden, maar het adres (de URL) van een bestand opgeven.
Copernica zal dan periodiek jouw importbestand van het opgegeven adres
downloaden en importeren. Dit kan over het FTP-protocol, maar de beveiligde
varianten SFTP en FTPS worden beide ook ondersteund.

Voor de rest zijn de importinstellingen voor periodieke imports gelijk aan
de instellingen bij geüploade bestanden. Ook hier kun je kolommen koppelen
en sleutelvelden opgeven. Het enige verschil is dat er een extra tabblad
"interval" beschikbaar is om in te stellen hoeveel tijd er tussen twee
imports moet zitten.

## Converteren van datumnotatie
De datumnotatie in Copernica is de JJJJ-MM-DD uu:mm:ss. Dit is een handige
notatie, omdat datums hierdoor makkelijk zijn te sorteren. Let wel op
dat je dezelfde notatie gebruikt in je invoerbestand en dat je in je
importbestand niet per ongeluk datums in DD-MM-JJ notaties hebt staan.

De importmodule heeft een optie om datums die in de verkeerde volgorde staan
automatisch te converteren zodat ze toch goed in Copernica komen te staan.
Dit is echter wel foutgevoelig: de datum 03-09-1980 kan immers zowel worden
geïnterpreteerd als 9 maart 1980 en als 3 september 1980. Ongeldige datums
worden genegeerd en als leeg bestand opgeslagen. Lege datumvelden mogen echter
niet bestaan in datumvelden, dus worden ze automatisch omgezet naar
0000-00-00 (00:00:00).

## Verkeerde import terugdraaien
Als je iets verkeerd doet, kun je zomaar je hele database overschrijven met
verkeerde gegevens. Goed opletten dus. Als het toch verkeerd is gegaan, kun
je dit met het volgende stappenplan herstellen:

Na een verkeerde import kun je een selectie aanmaken waarin je alle nieuwe
profielen opneemt. Je maakt hiervoor een selectie met een conditie van het
type "check op wijzigingen". Als type verandering kies je voor "het profiel
is aangemaakt" waarbij je de periode instelt waarin de import heeft
plaatsgevonden. Als de selectie klaar is met opbouwen kun je alle profielen
in deze selectie verwijderen via de optie "wijzigen/verwijderen meerdere
profielen".

Zijn er door de import bestaande profielen verkeerd gewijzigd? Het
terughalen van profieldata kan alleen per individueel profiel met de rollback
functie. Eventueel kun je Copernica vragen om een back-up van
de database terug te zetten. Hier zijn wel kosten aan verbonden.

## Importeren in de Marketing Suite
Klik op de database of collectie waar de import gestart voor dient te worden.
Klik op het **blauwe tandwiel** rechtsboven > **Importeren** >
**Nieuwe import aanmaken**. Geef de import een naam, kies het juiste
scheidingsteken en upload het bestand. Kies vervolgens de juiste opties zoals
hierboven beschreven.

## Importeren in de Publisher
Om een bestand te importeren dien je eerst een database te selecteren onder
**Profielen**. Je kunt daarna onder **Huidige weergave** de optie vinden om te
**exporteren of importeren**.

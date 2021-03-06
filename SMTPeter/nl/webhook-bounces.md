# Webhooks voor bounces

SMTPeter bewerkt normaal gesproken het *envelope* adres van alle e-mails
die middels SMTPeter worden verstuurd. Dit wordt gedaan om *bounces* te
traceren en ook om andere *events* te kunnen onderscheppen.
Naast dat SMTPeter alles automatisch ontvangt, kan je er voor kiezen om
zelf ook meldingen over *Webhooks* te ontvangen.


## Type meldingen

De webhook voor bounces traceert letterlijk _alle_ meldingen
die terug worden gestuurd naar het envelope adres. Dit betekent ook 
dat reguliere delivery status notifications, *out-of-office replies* 
en foutmeldingen worden teruggestuurd. Al deze type meldingen kun je 
ontvangen door de [webhook voor bounces](./webhooks) op te zetten.

## Bounces versus Delivery Status Notifications

SMTPeter verstuurt e-mails door middel van het SMTP protocol. Dit
protocol staat *remote servers* toe om een bericht te accepteren of
te weigeren. Geweigerde e-mails worden bijgeschreven op de *failure logfile*
en respectievelijk ook toegevoegd aan de *failure webhook* (zie diagram 1).

**Diagram 1**
<img style="float: center; max-width: 60%; max-height: 60%; margin-bottom: 20px;" src="Images/smtpeter-diagram-send-email.svg">

Echter, het is mogelijk dat een bericht initieel geaccepteerd wordt, 
maar dat de server achteraf toch nog een bounce e-mail verstuurd 
waarin mede wordt gedeeld dat het bericht toch is geweigerd. 
Deze vorm van bounces duiden op een Delivery Status Notification
en hebben een speciaal formaat. SMTPeter herkent ook deze type van bounces
en schrijft ze naar de *log files*. Ook de [failure webhook](webhook-failures)
wordt aangeroepen (zie diagram 2).

**Diagram 2**
<img style="float: center; max-width: 60%; max-height: 60%; margin-bottom: 20px;" src="Images/smtpeter-diagram-bounce.svg">

Naast deze standaard Delivery Status Notifications zijn er nog vele andere
berichten die terug worden gestuurd naar het envelope adres. Dit zijn 
bijvoorbeeld out-of-office e-mails, maar ook foutmeldingen over het 
feit dat de mailbox vol zit of het e-mailadres niet bestaat. Deze meldingen
komen van servers die het officiële Delivery Status Notification niet
respecteren. SMTPeter pakt deze meldingen ook gewoon op.

SMTPeter herkent dat deze meldingen niet naar de reguliere error log file
moeten worden geschreven en stuurt ze dus naar de bounce log file en 
consequent ook naar de bounce webhooks.


## Formaat

De bounce webhook wordt door middel van het HTTP POST mechanisme verstuurd. 
De volgende variabelen worden dan ingevoerd:

| Variabelen| Omschrijving                                                                      |
|-----------|-----------------------------------------------------------------------------------|
| id        | origineel message id van de bounce in kwestie                                     |
| recipient | e-mailadres waar de originele mail naartoe is verstuurd                           |
| mailfrom  | "MAIL FROM" adres dat is gebruikt voor aflevering van de inkomende bounce         |
| rcptto    | "RCPT TO" adres dat is gebruikt voor aflevering van de inkomende bounce           |
| mime      | de MIME data dat is verstuurd, dit is het daadwerkelijk ontvangen bounce bericht  |

De "ID" en "recipient" variabelen stellen je in staat om de inkomende bounce
te linken aan het oorspronkelijke bericht dat werd verstuurd. De "mailfrom", 
"rcptto" en "data" velden bevatten de melding die door SMTPeter is ontvangen.

## Meer informatie

* [Webhooks](./webhooks)
* [Webhookss instellen](./webhook-setup)

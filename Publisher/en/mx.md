# MX records

If you configure a [Sender Domain](./sender-domains.md), the Marketing Suite
dashboard shows a list of recommended [DNS](./dns.md) records that you should
copy to your DNS servers. Most of these recommendations are aliases (CNAME
records) that refer to records on the DNS servers of Copernica. However, there
is also an MX record in this list. This MX record should be created so that 
Copernica can process bounces and out-of-office replies. If you follow the
recommendation and create the required MX record, all bounces and most 
out-of-office are sent back to Copernica, where we can use them for statistics
and follow-up actions.

## Envelope addresses

To understand how this exactly works, we need to explain two important concepts
of email: envelope addresses and MX records. Let's start with envelope addresses.

Email messages normally have two different source addresses: the *from* address
that you can see in your email program, and a separate invisible *envelope* address.
This invisible address is normally not displayed to end users, because it is 
intended to be used by mail servers. If mail servers need to send messages to 
each other, like they do in case of a bounce, they use this special envelope address.

Mailings sent by Copernica use such a special envelope address. Besides the normal 
*from* address (like info@yourcompany.com), each message gets a unique *envelope* 
address (for example ui2ad8f9@feedback.yourcompany.com). The part in front of 
the '@' is a code that is unique for each addressee. When we receive a bounce that
is sent to such an address, we can easily link this bounce to the original message 
because of this unique identifier. 

## MX records

Email messages (remember that bounces are email messages too) are sent to email 
addresses. However, computers use IP addresses instead of email addresses to 
communicate with each other. If a server has to deliver an email message, the 
email address must therefore first be converted into an IP address. For this 
conversion MX records are used.

A MX record is a DNS setting that is used to specify the mail servers that are
responsible for handling incoming messages. A computer program that tries to
deliver an email fetches this MX record so that it can find out the IP address
to which the message should be delivered.

The envelope address that we use in mailings uses a subdomain of the main domain, 
like feedback.yourcompany.com. A server that tries to send a bounce to the
bounce address does a MX lookup for this subdomain. If you've followed the
recommendation from the dashboard and you've correctly configured the MX record,
the MX lookup succeeds and contains the address of Copernica's mail servers, so
that the bounce is sent to one of our servers where we can process it.

## Can't make MX records?

Not all DNS providers allow you to make MX records. If your domain is 
hosten under such a service it becomes a bit harder to follow the quick 
start instructions, because you can't make the MX records. Luckily there 
exists a workaround.

When the Copernica dashboard advises you to make a MX record you can make 
a CNAME record instead with the following scheme:

```text
<table>
    <tr>
        <td><strong>Advised MX record</strong></td>
        <td><strong>Alternative CNAME record</strong></td>
    </tr>
    <tr>
        <td>MX 0 ms.copernica.com</td>
        <td>CNAME feedback.copernica.com</td>
    </tr>
    <tr>
        <td>MX 0 mail.smtpeter.com</td>
        <td>CNAME smtpeter.com</td>
    </tr>
</table>
```

In the table above you can the MX record advised by the dashboard and 
the CNAME record you may use instead.

## More information

* [Sender domains](./sender-domains)
* [DMARC](./dmarc)
* [DKIM](./dkim)
* [SPF](./spf)

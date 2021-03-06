---

copyright:
  years: 2015, 2019
lastupdated: "2019-02-19"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}

<!-- Acrolinx: 2018-05-31 -->

# Account
{: #account}

Your account is your entry point for the {{site.data.keyword.cloudantfull}} API.
You access your account by using the address prefix
`https://$ACCOUNT.cloudant.com`.
Your {{site.data.keyword.cloudant_short_notm}} dashboard is always
`https://$ACCOUNT.cloudant.com/dashboard.html`.
{: shortdesc}

If you don't yet have an account, [sign up ![External link icon](../images/launch-glyph.svg "External link icon")](https://cloudant.com/sign-up/){: new_window}.

## Ping
{:  #ping}

To see whether your {{site.data.keyword.cloudant_short_notm}} account is accessible,
make a `GET` against `https://$ACCOUNT.cloudant.com`.
If you misspelled your account name,
you might get a [503 'service unavailable' error](/docs/services/Cloudant/api/Cloudant?topic=cloudant-http#http-status-codes).

_Example of connecting to your {{site.data.keyword.cloudant_short_notm}} account, by using HTTP:_

```HTTP
GET / HTTP/1.1
HOST: $ACCOUNT.cloudant.com
```
{: codeblock}

_Example of connecting to your {{site.data.keyword.cloudant_short_notm}} account, by using the command line:_

```sh
curl -u $ACCOUNT https://$ACCOUNT.cloudant.com
```
{: codeblock}

<!--

_Example of connecting to your {{site.data.keyword.cloudant_short_notm}} account, by using Javascript:_

```javascript
var nano = require('nano');
var account = nano("https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com");
account.request(function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{: codeblock}

-->

_Example of connecting to your {{site.data.keyword.cloudant_short_notm}} account, by using Python:_

```python
import cloudant
account = cloudant.Account(USERNAME)
ping = account.get()
print ping.status_code
# Expected return code: 200
```
{: codeblock}

## CORS
{: #cors-overview}

[Cross-origin resource sharing (CORS) ![External link icon](../images/launch-glyph.svg "External link icon")](http://www.w3.org/TR/cors/){: new_window} is a
mechanism that allows JavaScript from another domain to interact with data in
your {{site.data.keyword.cloudant_short_notm}} account.

For more information about CORS and {{site.data.keyword.cloudant_short_notm}}, see [CORS](/docs/services/Cloudant/api/cors.html).

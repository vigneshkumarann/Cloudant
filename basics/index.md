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

<!-- Acrolinx: 2018-05-07 -->

# {{site.data.keyword.cloudant_short_notm}} Basics
{: #ibm-cloudant-basics}

If it's your first time here,
scan this section before you scroll further.
{: shortdesc}

To understand the information on the following topics, we assume that you know some basic things about {{site.data.keyword.cloudantfull}}: 

- [Client Libraries](/docs/services/Cloudant/libraries/index.html#client-libraries)
- [API Reference](/docs/services/Cloudant/api/index.html##api-reference-overview)
- [Guides](acurl.html#authorized-curl-acurl-)

## Connecting to {{site.data.keyword.cloudant_short_notm}}

To access {{site.data.keyword.cloudant_short_notm}},
you must have either an [{{site.data.keyword.cloudant_short_notm}} account](/docs/services/Cloudant/api/account.html),
or an [{{site.data.keyword.cloud}} account](/docs/services/Cloudant/offerings/bluemix.html).

## HTTP API

All requests to {{site.data.keyword.cloudant_short_notm}} go over the web.
This means any system that can speak to the web can speak to {{site.data.keyword.cloudant_short_notm}}.
All language-specific libraries for {{site.data.keyword.cloudant_short_notm}} are really just wrappers that provide
some convenience and linguistic niceties to help you work with a simple API.
Many users choose to use raw HTTP libraries for working with {{site.data.keyword.cloudant_short_notm}}.

For more information about how {{site.data.keyword.cloudant_short_notm}} uses HTTP, see [HTTP ](/docs/services/Cloudant/api/http.html) in the API reference.

{{site.data.keyword.cloudant_short_notm}} supports the following HTTP request methods:

-   `GET`

    Request the specified item.
    As with normal HTTP requests,
    the format of the URL defines what is returned.
    With {{site.data.keyword.cloudant_short_notm}} this can include static items,
    database documents,
    and configuration and statistical information.
    In most cases the information is returned in the form of a JSON document.

-   `HEAD`

    The `HEAD` method is used to get the HTTP header of a `GET` request without the body of the response.

-   `POST`

    Upload data.
    Within {{site.data.keyword.cloudant_short_notm}}'s API,
    the `POST` method is used to set values,
    upload documents,
    set document values,
    and start some administration commands.

-   `PUT`

    Used to 'store' a specific resource.
    In {{site.data.keyword.cloudant_short_notm}}'s API,
    `PUT` is used to create new objects,
    including databases,
    documents,
    views,
    and design documents.

-   `DELETE`

    Deletes the specified resource,
    including documents,
    views,
    and design documents.

-   `COPY`

    A special method that can be used to copy documents and objects.

If the client (such as some web browsers) does not support using these HTTP methods,
`POST` can be used instead with the `X-HTTP-Method-Override` request header set to the actual HTTP method.

### Method not allowed error

If you use an unsupported HTTP request type with a URL that does not support the specified type,
a [405](/docs/services/Cloudant/api/http.html#http-status-codes) error is returned,
listing the supported HTTP methods, as shown in the following example.

_Example error message in response to an unsupported request:_

```json
{
    "error":"method_not_allowed",
    "reason":"Only GET,HEAD allowed"
}
```
{: codeblock}

## JSON
{: #json-overview}

{{site.data.keyword.cloudant_short_notm}} stores documents using JSON (JavaScript Object Notation) encoding,
so anything encoded into JSON can be stored as a document.
Files containing media,
such as images,
videos,
and audio,
are called BLOBs (Binary Large OBjects),
and can be stored as attachments associated with documents.

More information about JSON can be found in the [JSON Guide](/docs/services/Cloudant/guides/json.html).

<div id="distributed"></div>

## Distributed Systems

{{site.data.keyword.cloudant_short_notm}}'s API enables you to interact with a collaboration of numerous machines,
called a cluster.
The machines in a cluster must be in the same datacenter,
but can be within different 'pods' in that datacenter.
Using different pods helps improve the High Availability characteristics of {{site.data.keyword.cloudant_short_notm}}.

An advantage of clustering is that when you need more computing capacity,
you just add more machines.
This is often more cost-effective and fault-tolerant than scaling up or enhancing an existing single machine.

For more information about {{site.data.keyword.cloudant_short_notm}} and distributed system concepts,
see the [CAP Theorem](/docs/services/Cloudant/guides/cap_theorem.html) guide.

## Replication

[Replication](/docs/services/Cloudant/api/replication.html) is a procedure followed by {{site.data.keyword.cloudant_short_notm}},
[CouchDB ![External link icon](../images/launch-glyph.svg "External link icon")](http://couchdb.apache.org/){: new_window},
[PouchDB ![External link icon](../images/launch-glyph.svg "External link icon")](http://pouchdb.com/){: new_window},
and other distributed databases.
Replication synchronizes the state of two databases so that their contents are identical.

You can replicate continuously.
This means that a target database updates every time the source database changes.
Continuous replication can be used for backups of data,
aggregating data across multiple databases,
or for sharing data.

However,
continuous replication means testing continuously for any source database changes.
This testing requires continuous internal calls,
which might impact performance or the cost of using the database.

Continuous replication can result in many internal calls. These calls might affect costs for multi-tenant users of {{site.data.keyword.cloudant_short_notm}} systems. Continuous replication is disabled by default.
{: note}


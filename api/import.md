---
description: 'Manage Imports, which are collections of Invoices.'
---

# Import

{% api-method method="get" host="https://api.clubcollect.com/api" path="/v2/imports/:id" %}
{% api-method-summary %}
Show Import
{% endapi-method-summary %}

{% api-method-description %}
Fetch an Import’s details.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Import ID, supplied by ClubCollect.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Partner API Key.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Import successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
  "import_id": "a1f3216863ba5d5424dcbace46ab37be98d70c92",
  "title": "Membership fees 2016/02",
  "transmitted": true|false,
  "transmitted_at": "2017-05-16T08:57:02+00:00",
  "prepaid_amount_cents": 123,
  "prepaid_amount_currency": "EUR|GBP|CHF",
  "settled_amount_cents": 456,
  "settled_amount_currency": "EUR|GBP|CHF",
  "invoice_ids": [
    "47417520982b90764d0067d529691934e6ec3a42",
    "c0009400834121ded4cdd5a623da52f12c737262",
    "43cf319011497b1b40d81e341a652b04866a2d0b"
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find an Import with this ID.
{% endapi-method-response-example-description %}

```javascript
{
    "errors": "not_found"
}
```
{% endapi-method-response-example %}

{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
This endpoint will be deprecated soon in favour of manually transmitting an Import via the ClubCollect User Interface. This gives treasurers the opportunity to configure settings correctly which is not possible via the API.
{% endhint %}


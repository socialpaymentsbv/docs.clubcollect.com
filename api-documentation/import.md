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
    "errors": "invalid_import_id"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.clubcollect.com/api" path="/v2/imports" %}
{% api-method-summary %}
Create Import
{% endapi-method-summary %}

{% api-method-description %}
Create a new, empty Import.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Partner API Key.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="title" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="company\_id" type="string" required=true %}
Company to which the Import should belong.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "import_id": "a1f3216863ba5d5424dcbace46ab37be98d70c92",
  "title": "Membership fees 2016/02",
  "transmitted": false,
  "transmitted_at": null,
  "prepaid_amount_cents": 0,
  "prepaid_amount_currency": "EUR",
  "settled_amount_cents": 0,
  "settled_amount_currency": "EUR",
  "invoice_ids": [
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_company_id"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="warning" %}
The following `/imports/:id/transmit` endpoint will be deprecated soon in favour of manually transmitting an Import via the ClubCollect User Interface. This gives treasurers the opportunity to configure settings correctly which is not possible via the API.
{% endhint %}

{% api-method method="put" host="https://api.clubcollect.com/api" path="/v2/imports/:id/transmit" %}
{% api-method-summary %}
Transmit Import
{% endapi-method-summary %}

{% api-method-description %}
Instruct ClubCollect to transmit the Import, initiating the invoice collection process.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Import ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Partner API Key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Batch successfully transmitted.
{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_import_id"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "import_already_transmitted"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
Ensure you have finished creating all Invoices for this Import before calling this method. It is not possible to change or add more Invoices to an Import after the Import has been transmitted.
{% endhint %}

{% api-method method="delete" host="https://api.clubcollect.com/api" path="/v2/imports/:id" %}
{% api-method-summary %}
Delete Import
{% endapi-method-summary %}

{% api-method-description %}
Deletes an import and all the invoices that have been created for the import.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Import ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Partner API Key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}
Batch successfully deleted.
{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_import_id"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "import_already_transmitted"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


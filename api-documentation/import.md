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

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
ApiKey &lt;api\_key&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=false %}
Partner API Key (Deprecated)
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
  "expected_invoices_count": 3,
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
{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
ApiKey &lt;api\_key&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=false %}
Partner API Key (Deprecated)
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="title" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="company\_id" type="string" required=true %}
Company to which the Import should belong.
{% endapi-method-parameter %}

{% api-method-parameter name="expected_invoices_count" type="string" required=false %}
Number of invoices expected to be added to this import. If provided the Import
cannot be transmitted from the ClubCollect User Interface until all invoices
are created.
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
  "expected_invoices_count": 0,
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

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
ApiKey &lt;api\_key&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=false %}
Partner API Key (Deprecated)
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Batch successfully transmitted.
{% endapi-method-response-example-description %}

```javascript
{
  "import_id": "a1f3216863ba5d5424dcbace46ab37be98d70c92",
  "title": "Membership fees 2016/02",
  "transmitted": true,
  "transmitted_at": "2016-02-12T20:55:19Z",
  "prepaid_amount_cents": 0,
  "prepaid_amount_currency": "EUR",
  "settled_amount_cents": 0,
  "settled_amount_currency": "EUR",
  "expected_invoices_count": 0,
  "invoice_ids": [
  ]
}
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

{% api-method method="put" host="https://api.clubcollect.com/api" path="/v2/imports/:id" %}
{% api-method-summary %}
Update Import
{% endapi-method-summary %}

{% api-method-description %}
Update an import.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}

{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Import ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
ApiKey &lt;api\_key&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=false %}
Partner API Key (Deprecated)
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="expected_invoices_count" type="string" required=false %}
Number of invoices expected to be added to this import. If provided the Import
cannot be transmitted from the ClubCollect User Interface until all invoices
are created.
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
  "expected_invoices_count": 0,
  "invoice_ids": [
  ]
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_company_id"
}
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

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
ApiKey &lt;api\_key&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=false %}
Partner API Key (Deprecated)
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

{% api-method method="get" host="https://api.clubcollect.com/api" path="/v2/companies/:id/imports" %}
{% api-method-summary %}
Fetch Company Imports
{% endapi-method-summary %}

{% api-method-description %}
Returns the list of import batches created by a company, paginated and sorted in ascending order, i.e. from oldest to newest.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the company for which batches are requested.
{% endapi-method-parameter %}

{% api-method-parameter name="page_number" type="string" required=false %}
Page number requested. If not specified, default to `1`.
{% endapi-method-parameter %}

{% api-method-parameter name="page_size" type="string" required=false %}
Number of results per page. If not specified, default to `30`.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Authorization" type="string" required=true %}
ApiKey &lt;api\_key&gt;
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=false %}
Partner API Key (Deprecated)
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
"imports": [
  {
   "company_id": "477b4e18deb43367449d1ca74dc7f67b91e68ad3",
   "import_id": "78d366d133d6e26e32106b645f92c899f410897c",
   "title": "Membership fee 2019/1",
   "transmitted": "true",
   "transmitted_at": "2019-09-12T20:55:19Z"
  },
  {
   "company_id": "477b4e18deb43367449d1ca74dc7f67b91e68ad3",
   "import_id": "bffce68a7d109a9de3bfd3f3baacd06516492272",
   "title": "Membership fee 2019/2",
   "transmitted": "true",
   "transmitted_at": "2019-09-116T15:53:08Z"
  },
]
"page": {
  "page_number": 1,
  "total_pages": 1
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Company ID does not exist.
{% endapi-method-response-example-description %}

```javascript
{
  "error": "not_found"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

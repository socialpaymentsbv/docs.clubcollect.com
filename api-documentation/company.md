---
description: 'Manage Companies, the entity representing an individual organisation.'
---

# Company

{% hint style="danger" %}
This endpoint is not yet operational and is thus subject to change.
{% endhint %}

{% api-method method="get" host="https://app.clubcollect.com/api" path="/v2/companies/:id" %}
{% api-method-summary %}
Show Company
{% endapi-method-summary %}

{% api-method-description %}
Fetch a Company’s details.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Company ID, supplied by ClubCollect.
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
Company successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
  "company_id": "a1f3216863ba5d5424dcbace46ab37be98d70c92", 
  "name": "Amsterdam Collectors FC",
  "brand": "clubcollect",
  "email": "admin@amscollectors.nl",
  "locale": "nl",
  "address1": "Sint Pieterspoortsteeg",
  "address2": "2nd floor",
  "house_number": "2",
  "zipcode": "1012 HM",
  "city": "Amsterdam",
  "country_code": "NL",
  "currency": "EUR"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a Company with this ID.
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

{% api-method method="post" host="https://app.clubcollect.com/api" path="/v2/companies" %}
{% api-method-summary %}
Create Company
{% endapi-method-summary %}

{% api-method-description %}
Create a new Company.
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
{% api-method-parameter name="name" type="string" required=true %}
Name of Company.
{% endapi-method-parameter %}

{% api-method-parameter name="brand" type="string" required=true %}
Brand code. From `{ clubbaseio knltb dtb clubcollect clubcollectde }`.
{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=true %}
Email address of Company contact.
{% endapi-method-parameter %}

{% api-method-parameter name="locale" type="string" required=true %}
Default locale for Company members. From `{ de en fr it nl }`.
{% endapi-method-parameter %}

{% api-method-parameter name="country\_code" type="string" required=true %}
Country of official Company registration. From `{ AT BE CH DE GB IE NL }`.
{% endapi-method-parameter %}

{% api-method-parameter name="address1" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="address2" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="house\_number" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="zipcode" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="city" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="vat\_percentage" type="number" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="partnership\_page\_url" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="currency" type="string" required=true %}
Currency. From `{ EUR GBP CHF }`.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Company successfully created.
{% endapi-method-response-example-description %}

```javascript
{
  "company_id": "a1f3216863ba5d5424dcbace46ab37be98d70c92",
  "name": "Amsterdam Collectors FC",
  "brand": "clubcollect",
  "email": "admin@amscollectors.nl",
  "locale": "nl",
  "address1": "Sint Pieterspoortsteeg",
  "address2": "2nd floor",
  "house_number": "2",
  "zipcode": "1012 HM",
  "city": "Amsterdam",
  "country_code": "NL",
  "currency": "EUR"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://app.clubcollect.com/api" path="/v2/companies/:id" %}
{% api-method-summary %}
Update Company
{% endapi-method-summary %}

{% api-method-description %}
Update Company details.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Company ID, supplied by ClubCollect.
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
{
  "company_id": "a1f3216863ba5d5424dcbace46ab37be98d70c92",
  "name": "Amsterdam Collectors FC",
  "brand": "clubcollect",
  "email": "admin@amscollectors.nl",
  "locale": "nl",
  "address1": "Sint Pieterspoortsteeg",
  "address2": "2nd floor",
  "house_number": "2",
  "zipcode": "1012 HM",
  "city": "Amsterdam",
  "country_code": "NL",
  "currency": "EUR"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Parameters for `PUT` are the same as `POST`.


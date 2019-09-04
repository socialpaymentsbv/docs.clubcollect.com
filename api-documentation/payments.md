---
description: Use ClubCollect as your payment provider
---

# Payments \(WIP\)

{% api-method method="get" host="https://app.clubcollect.com/api/v2/payments" path="/ideal" %}
{% api-method-summary %}
ideal
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows to start a new iDEAL payment and redirects the user to the payment page.  
  
For new payments, an invoice is generated first. Invoices are grouped in batches, per month. These batches can be found on  \`https://app.clubcollect.com/treasurer/import\_batches\`, their name it's \`iDEAL \(&lt;year&gt;-&lt;month&gt;\)\`, e.g. \`iDEAL \(2019-08\)\`.  
  
It's also possible to start the payment process for an existing invoice. When a payment isn't completed by the user, the invoice ID can be given to pay the same invoice instead of creating a new one.  
  
The partner is responsible to add to the URL any parameters that might be needed to complete the payment process on their side. Billin
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="prefix" type="string" required=false %}
Prefix of the name of the payee.
{% endapi-method-parameter %}

{% api-method-parameter name="locale" type="string" required=false %}
Language that will be used in the payment process and in further communications with the member, if there were any. If not given, the company default locale will be used.
{% endapi-method-parameter %}

{% api-method-parameter name="external\_invoice\_number" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="payment\_reference" type="string" required=false %}
Reference of the payment, will be used a description of the invoice line.
{% endapi-method-parameter %}

{% api-method-parameter name="first\_name" type="string" required=false %}
First name of the payee.
{% endapi-method-parameter %}

{% api-method-parameter name="invoice\_id" type="string" required=false %}
ID of the invoice that is going to be paid. ClubCollect will return the ID in every redirect URL. 
{% endapi-method-parameter %}

{% api-method-parameter name="company\_id" type="string" required=true %}
Company to which the payment and the invoice belong.
{% endapi-method-parameter %}

{% api-method-parameter name="signature" type="string" required=true %}
Used by ClubCollect to authenticate the request and ensure data integrity. 
{% endapi-method-parameter %}

{% api-method-parameter name="redirect\_url" type="string" required=true %}
URL to which the user should be redirected after the payment process has finished. 
{% endapi-method-parameter %}

{% api-method-parameter name="last\_name" type="string" required=false %}
Last name of the payee. Only required for new payments.
{% endapi-method-parameter %}

{% api-method-parameter name="amount\_cents" type="integer" required=false %}
Amount in cents that is going to be paid. Only required for new payments.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Cake successfully retrieved.
{% endapi-method-response-example-description %}

```javascript
{
    "name": "Cake's name",
    "recipe": "Cake's recipe name",
    "cake": "Binary cake"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Could not find a cake matching this query.
{% endapi-method-response-example-description %}

```javascript
{
    "message": "Ain't no cake like that."
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}




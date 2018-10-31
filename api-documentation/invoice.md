---
description: Manage Invoices.
---

# Invoice

{% api-method method="get" host="https://api.clubcollect.com/api" path="/v2/invoices/:id" %}
{% api-method-summary %}
Show Invoice
{% endapi-method-summary %}

{% api-method-description %}
Fetch Invoice details.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Invoice ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=false %}
Must be `application/json`.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Partner API Key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "import_id": "...", 
  "external_invoice_number": "2014-342-545", 
  "direct_debit_iban": "...", 
  "federation_membership_number": "...", 
  "club_membership_number": "...", 
  "customer": {
    "name": { 
      "prefix": "Mr", 
      "first_name": "Joe", 
      "infix": "van der", 
      "last_name": "Doe"
    },
    "address": { 
      "address1": "3rd Avenue", 
      "address2": "", 
      "locality": "", 
      "house_number": "1500", 
      "state": "", 
      "zipcode": "10010", 
      "city": "Amsterdam", 
      "country_code": "NL"
    },
    "email": { 
      "email_address": "joe@example.com"
    },
    "phone": { 
      "phone_number": "562-756-2233", 
      "country_code": "NL"
    } 
  }, 
  "invoice_lines": [        
    {
      "invoice_line_id": "...",            
      "type": "INVOICE-LINE",            
      "amount_cents": 10000,            
      "description": "Membership fee",            
      "date": "..."        
    },        
    {
      "invoice_line_id": "...",           
      "type": "CREDIT-LINE",            
      "amount_cents": -1000,           
      "description": "Deduction",            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "PAYMENT-LINE",           
      "amount_cents": 123,            
      "description": "...",            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "CHARGEBACK-LINE",            
      "amount_cents": 123,           
      "description": "...",            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",           
      "type": "CHARGEBACK-FEE-LINE",            
      "amount_cents": 123,           
      "description": "...",            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "CHARGEBACK-FEE-PAYMENT-LINE",            
      "amount_cents": 123,            
      "description": "...",            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "LATE-PAYMENT-FEE-LINE",            
      "amount_cents": 123,            
      "description": "...",            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "LATE-PAYMENT-FEE-PAYMENT-LINE",            
      "amount_cents": 123,            
      "description": "...",            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "INSTALLMENT-FEE-LINE",            
      "amount_cents": 123,            
      "description": "...",            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "INSTALLMENT-FEE-PAYMENT-LINE",           
      "amount_cents": 123,            
      "description": "...",            
      "date": "..."        
    }    
  ],
  "amount_total_cents": "...", 
  "messages": [
    { 
      "message_id": "...", 
      "type": "EMAIL|SMS|LETTER", 
      "description": "...", 
      "date": "..."
    },
    { 
      "message_id": "...", 
      "type": "EMAIL|SMS|LETTER",
      "description": "...", 
      "date": "..."} 
  ], 
  "tickets": [
    { 
      "ticket_id": "...", 
      "message": "I don't want to pay", 
      "sender": "CUSTOMER", 
      "date": "..."
    },
    { 
      "ticket_id": "...", 
      "message": "You really must pay", 
      "sender": "COMPANY", 
      "date": "..."} 
  ], 
  "retracted_at": null | "...", 
  "retraction_reason": null | "...", 
  "show_retraction_reason_to_customer": true | false
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_invoice_id"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% hint style="info" %}
A Partner usually calls the `GET /v2/invoices/:id` method in response to a notification sent by ClubCollect about an update to an Invoice.
{% endhint %}

{% api-method method="post" host="https://api.clubcollect.com/api" path="/v2/invoices" %}
{% api-method-summary %}
Create Invoice
{% endapi-method-summary %}

{% api-method-description %}
Create an Invoice with one or more Invoice Lines.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
Must be: `application/json`.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Partner API Key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="direct\_debit\_iban" type="string" required=false %}
When supplied, will be accepted and added to the Invoice only if it is a valid IBAN.
{% endapi-method-parameter %}

{% api-method-parameter name="invoice\_lines\[\].invoice\_line\_id" type="string" required=false %}
Optionally specify a custom identifier to overwrite an otherwise randomly generated identifier.
{% endapi-method-parameter %}

{% api-method-parameter name="amount\_total\_cents" type="number" required=true %}
Must be equal to the sum of the amounts of the Invoice Lines. May be zero or negative.
{% endapi-method-parameter %}

{% api-method-parameter name="invoice\_lines" type="array" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.country\_code" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.city" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.zipcode" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.zipcode" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.address1" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.phone.country\_code" type="string" required=true %}
May be empty if \`email\_address\` is provided\`
{% endapi-method-parameter %}

{% api-method-parameter name="customer.phone.phone\_number" type="string" required=true %}
May be empty if \`email\_address\` is provided.
{% endapi-method-parameter %}

{% api-method-parameter name="customer.email.email\_address" type="string" required=true %}
May be empty if \`phone\_number\` is provided.
{% endapi-method-parameter %}

{% api-method-parameter name="customer.name.last\_name" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="external\_invoice\_number" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="import\_id" type="string" required=true %}
ID of Import to which the Invoice should belong.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "import_id": "...", 
  "external_invoice_number": "2014-342-545", 
  "direct_debit_iban": "...", 
  "federation_membership_number": "...", 
  "club_membership_number": "...", 
  "customer": {
    "name": { 
      "prefix": "Mr", 
      "first_name": "Joe", 
      "infix": "van der", 
      "last_name": "Doe"
    },
    "address": { 
      "address1": "3rd Avenue", 
      "address2": "", 
      "locality": "", 
      "house_number": "1500", 
      "state": "", 
      "zipcode": "10010", 
      "city": "Amsterdam", 
      "country_code": "NL"
    },
    "email": { 
      "email_address": "joe@example.com"
    },
    "phone": { 
      "phone_number": "562-756-2233", 
      "country_code": "NL"
    } 
  }, 
  "invoice_lines": [        
    {
      "invoice_line_id": "...",            
      "type": "INVOICE-LINE",            
      "amount_cents": 10000,            
      "description": "Membership fee",            
      "date": "..."        
    },
    { 
      "invoice_line_id": "...", 
      "amount_cents": -1000, 
      "description": "Deduction",
      "date": "..." 
    }
  ],
  "amount_total_cents": 9000,
  "tickets": [], 
  "messages": []
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Example Request Body

```javascript
{
  "import_id": "...", 
  "external_invoice_number": "2014-342-545", 
  "direct_debit_iban": "...", 
  "federation_membership_number": "...", 
  "club_membership_number": "...", 
  "customer": {
    "name": { 
      "prefix": "Mr", 
      "first_name": "Joe", 
      "infix": "van der", 
      "last_name": "Doe"
    },
    "address": { 
      "address1": "3rd Avenue", 
      "address2": "", 
      "locality": "", 
      "house_number": "1500", 
      "state": "", 
      "zipcode": "10010", 
      "city": "Amsterdam", 
      "country_code": "NL"
    },
    "email": { 
      "email_address": "joe@example.com"
    },
    "phone": { 
      "phone_number": "562-756-2233", 
      "country_code": "NL"
    } 
  }, 
  "invoice_lines": [        
    {
      "invoice_line_id": "...",            
      "type": "INVOICE-LINE",            
      "amount_cents": 10000,            
      "description": "Membership fee",            
      "date": "..."        
    },
    { 
      "invoice_line_id": "...", 
      "amount_cents": -1000, 
      "description": "Deduction",
      "date": "..." 
    }
  ],
  "amount_total_cents": 9000
}
```

#### Error Messages

* `invalid_import_id`: No import with this ID could be found.
* `invalid_external_invoice_number`: formatting error: min. 1 character.
* `invalid_customer_last_name`: Last name may not be empty.
* `invalid_customer_email`: Email address may not be empty if no phone number is provided.
* `invalid_customer_phone`: Phone number may not be empty if no email address is provided.
* `invalid_customer_address`: Address may not be empty if neither an email address nor phone number is provided.
* `invalid_amount_total_cents`: `amount_total_cents` is not equal to the total of all invoice line amounts.
* `invalid_content_type`: `Content-Type: application/json` must be provided. 

{% hint style="info" %}
**Note** the total may be zero \(nothing to receive\) or negative \(something to receive\).
{% endhint %}

{% hint style="info" %}
**Note** at least one of:

* `customer.email.email_address`
* `customer.phone.*`
* `customer.address.*`

must be provided. i.e. there must be a way for us to contact the Customer via email, phone or postal mail.
{% endhint %}



{% api-method method="put" host="https://api.clubcollect.com/api" path="/v2/invoices/:id" %}
{% api-method-summary %}
Update Invoice
{% endapi-method-summary %}

{% api-method-description %}
Update a subset of Invoice attributes.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Invoice ID
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
Must be: `application/json`.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Partner API Key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "import_id": "...", 
  "external_invoice_number": "2014-342-545", 
  "direct_debit_iban": "...", 
  "federation_membership_number": "...", 
  "club_membership_number": "...", 
  "customer": {
    "name": { 
      "prefix": "Mr", 
      "first_name": "Joe", 
      "infix": "van der", 
      "last_name": "Doe"
    },
    "address": { 
      "address1": "3rd Avenue", 
      "address2": "", 
      "locality": "", 
      "house_number": "1500", 
      "state": "", 
      "zipcode": "10010", 
      "city": "Amsterdam", 
      "country_code": "NL"
    },
    "email": { 
      "email_address": "joe@example.com"
    },
    "phone": { 
      "phone_number": "562-756-2233", 
      "country_code": "NL"
    } 
  }, 
  "invoice_lines": [        
    {
      "invoice_line_id": "...",            
      "type": "INVOICE-LINE",            
      "amount_cents": 10000,            
      "description": "Membership fee",            
      "date": "..."        
    },
    { 
      "invoice_line_id": "...", 
      "amount_cents": -1000, 
      "description": "Deduction",
      "date": "..." 
    }
  ],
  "amount_total_cents": 9000,
  "tickets": [], 
  "messages": []
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_invoice_id"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_external_invoice_number"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Example Request Body

```javascript
{
  "external_invoice_number": "2014-342-545", 
  "direct_debit_iban": "...", 
  "federation_membership_number": "...", 
  "club_membership_number": "...", 
  "customer": {
    "name": { 
      "prefix": "Mr", 
      "first_name": "Joe", 
      "infix": "van der", 
      "last_name": "Doe"
    },
    "address": { 
      "address1": "3rd Avenue", 
      "address2": "", 
      "locality": "", 
      "house_number": "1500", 
      "state": "", 
      "zipcode": "10010", 
      "city": "Amsterdam", 
      "country_code": "NL"
    },
    "email": { 
      "email_address": "joe@example.com"
    },
    "phone": { 
      "phone_number": "562-756-2233", 
      "country_code": "NL"
    } 
  },
}
```

#### Error Messages

* `invalid_invoice_id`: No invoice with this `invoice_id` could be found.
* `invalid_external_invoice_number`: formatting error: min. 1 character.
* `invalid_customer_last_name`: Last name may not be empty.
* `invalid_customer_email`: Email address may not be empty if no phone number is provided.
* `invalid_customer_phone`: Phone number may not be empty if no email address is provided.
* `invalid_content_type`: `Content-Type: application/json` must be provided.

{% api-method method="post" host="https://api.clubcollect.com/api" path="/v2/invoices/:id/credit" %}
{% api-method-summary %}
Credit Invoice
{% endapi-method-summary %}

{% api-method-description %}
Create a Credit Invoice for an existing Invoice. The Credit Invoice may contain one or more Invoice Lines. You cannot credit a Credit Invoice. Positive Invoice Line amounts are allowed provided the total amount is negative.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Invoice ID for the Invoice to be credited.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
Must be: `application/json`.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Partner API Key
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="amount\_total\_cents" type="number" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="invoice\_lines" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="external\_invoice\_number" type="array" required=true %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```
{
  "import_id": "...", 
  "external_invoice_number": "2014-342-545", 
  "direct_debit_iban": "...", 
  "federation_membership_number": "...", 
  "club_membership_number": "...", 
  "customer": {
    "name": { 
      "prefix": "Mr", 
      "first_name": "Joe", 
      "infix": "van der", 
      "last_name": "Doe"
    },
    "address": { 
      "address1": "3rd Avenue", 
      "address2": "", 
      "locality": "", 
      "house_number": "1500", 
      "state": "", 
      "zipcode": "10010", 
      "city": "Amsterdam", 
      "country_code": "NL"
    },
    "email": { 
      "email_address": "joe@example.com"
    },
    "phone": { 
      "phone_number": "562-756-2233", 
      "country_code": "NL"
    } 
  }, 
  "invoice_lines": [        
    {
      "invoice_line_id": "...",            
      "type": "INVOICE-LINE",            
      "amount_cents": 10000,            
      "description": "Membership fee",            
      "date": "..."        
    },
    { 
      "invoice_line_id": "...", 
      "amount_cents": -1000, 
      "description": "Deduction",
      "date": "..." 
    }
  ],
  "amount_total_cents": 9000,
  "tickets": [], 
  "messages": []
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_invoice_id"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_external_invoice_number"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

#### Example Request Body

```javascript
{ 
  "external_invoice_number": "2014-342-545", 
  "invoice_lines": [ 
    {
      "amount_cents": -10000,
      "description": "Credit membership fee" 
    } 
  ], 
  "amount_total_cents": 0
}
```

#### Error Messages

* `invalid_invoice_id`: No invoice with this `invoice_id` could be found.
* `invalid_external_invoice_number`: min. 1 character
* `invalid_invoice_lines`: min. 1 line
* `invalid_amount_total_cents`: should be the total of all invoice line amounts
* `invalid_credit_amount`: the total amount credited should be negative
* `invalid_content_type`: `Content-Type: application/json` must be provided.
* `payment_in_progress`: An invoice can't be credited or retracted if there's a payment in progress


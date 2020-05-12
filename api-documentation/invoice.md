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
  "invoice_id": "...",
  "import_id": "...",
  "external_invoice_number": "2014-342-545",
  "reference": "ba6fe77",
  "invoice_number": "123456",
  "direct_debit_iban": "...",
  "federation_membership_number": "...",
  "club_membership_number": "...",
  "customer": {
    "name": {
      "prefix": "Mr",
      "first_name": "Joe",
      "infix": "van der",
      "last_name": "Doe",
      "organization": "TheClub"
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
      "payment_method": "ideal|bacs|bancontact|credit_card|sdd|bank_transfer",
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
      "payment_method": "ideal|bacs|bancontact|credit_card|sdd|bank_transfer",
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
      "payment_method": "ideal|bacs|bancontact|credit_card|sdd|bank_transfer",
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
**Note** the date format is `ISO 8601`.
{% endhint %}

{% hint style="info" %}
**Note** a Partner usually calls the `GET /v2/invoices/:id` method in response to a notification sent by ClubCollect about an update to an Invoice.
{% endhint %}


{% hint style="info" %}
**Note** To get a list of possible values for invoice lines types see the Invoice Line documentation.
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
{% api-method-parameter name="locale" type="string" required=false %}
When supplied, the invoice's locale will be set to this value. From `{ de en fr it nl }`
{% endapi-method-parameter %}

{% api-method-parameter name="direct\_debit\_iban" type="string" required=false %}
When supplied, will be accepted and added to the Invoice only if it is a valid IBAN.
{% endapi-method-parameter %}

{% api-method-parameter name="federation\_membership\_number" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="club\_membership\_number" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="invoice\_lines\[\].invoice\_line\_id" type="string" required=false %}
Optionally specify a custom identifier to overwrite an otherwise randomly generated identifier. If given, the partner must ensure that the ID is unique. Requests with duplicate IDs will be rejected.
{% endapi-method-parameter %}

{% api-method-parameter name="amount\_total\_cents" type="number" required=true %}
Must be equal to the sum of the amounts of the Invoice Lines. May be zero or negative.
{% endapi-method-parameter %}

{% api-method-parameter name="invoice\_lines" type="array" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.country\_code" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.city" type="string" required=true %}
May be empty if \`email\_address\` or \`phone\_number\` is provided\`
{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.zipcode" type="string" required=true %}
May be empty if \`email\_address\` or \`phone\_number\` is provided\`
{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.address1" type="string" required=true %}
May be empty if \`email\_address\` or \`phone\_number\` is provided\`
{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.address2" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.house\_number" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.house\_number\_extension" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.locality" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.state" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.phone.country\_code" type="string" required=true %}
May be empty if \`email\_address\` or a postal address is provided\`
{% endapi-method-parameter %}

{% api-method-parameter name="customer.phone.phone\_number" type="string" required=true %}
May be empty if \`email\_address\` or a postal address is provided.
{% endapi-method-parameter %}

{% api-method-parameter name="customer.email.email\_address" type="string" required=true %}
May be empty if \`phone\_number\` or a postal address is provided.
{% endapi-method-parameter %}

{% api-method-parameter name="customer.name.last\_name" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.name.organization" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="external\_invoice\_number" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="reference" type="string" required=false %}

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
  "invoice_id": "...",
  "import_id": "...",
  "external_invoice_number": "2014-342-545",
  "reference": "ba6fe77",
  "invoice_number": "123456",
  "direct_debit_iban": "...",
  "federation_membership_number": "...",
  "club_membership_number": "...",
  "customer": {
    "name": {
      "prefix": "Mr",
      "first_name": "Joe",
      "infix": "van der",
      "last_name": "Doe",
      "organization": "TheClub"
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

## Example Request Body

```javascript
{
  "import_id": "...",
  "external_invoice_number": "2014-342-545",
  "reference": "ba6fe77",
  "direct_debit_iban": "...",
  "federation_membership_number": "...",
  "club_membership_number": "...",
  "locale": "en",
  "customer": {
    "name": {
      "prefix": "Mr",
      "first_name": "Joe",
      "infix": "van der",
      "last_name": "Doe",
      "organization": "TheClub"
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

## Error Messages

* `invalid_import_id`: No import with this ID could be found.
* `invalid_external_invoice_number`: formatting error: min. 1 character.
* `invalid_customer_last_name`: Last name may not be empty.
* `invalid_customer_email`: Email address may not be empty if no phone number is provided.
* `invalid_customer_phone`: Phone number may not be empty if no email address is provided.
* `invalid_customer_address`: Address may not be empty if neither an email address nor phone number is provided.
* `invalid_amount_total_cents`: `amount_total_cents` is not equal to the total of all invoice line amounts.
* `duplicate_invoice_line_id`: The `duplicate_invoice_line_id` provided was already used for another invoice line.
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

{% hint style="info" %}
**Note** It's not possible to add or delete invoice lines for an existing invoice. If an invoice is incorrectly created with a wrong amount outstanding (or the invoice becomes invalid for some reason after it's transmitted), the partner can credit it using `/credit_and_retract` endpoint. 
{% endhint %}

{% api-method method="put" host="https://api.clubcollect.com/api" path="/v2/invoices/:id" %}
{% api-method-summary %}
Update Invoice
{% endapi-method-summary %}

{% api-method-description %}
Update a subset of Invoice attributes.

{% hint style="info" %}
**Note** The invoice lines can't be updated, only the attributes relative to the recipient of the invoice can be updated.
{% endhint %}

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

{% api-method-body-parameters %}
{% api-method-parameter name="locale" type="string" required=false %}
When supplied, the invoice's locale will be set to this value. From `{ de en fr it nl }`
{% endapi-method-parameter %}

{% api-method-parameter name="direct\_debit\_iban" type="string" required=false %}
When supplied, will be accepted and added to the Invoice only if it is a valid IBAN.
{% endapi-method-parameter %}

{% api-method-parameter name="federation\_membership\_number" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="club\_membership\_number" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.country\_code" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.city" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.zipcode" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.address1" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.address2" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.house\_number" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.house\_number\_extension" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.locality" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.address.state" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.phone.country\_code" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.phone.phone\_number" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.email.email\_address" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.name.last\_name" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="customer.name.organization" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="external\_invoice\_number" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="reference" type="string" required=false %}

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
  "reference": "ba6fe77",
  "invoice_number": "123456",
  "direct_debit_iban": "...",
  "federation_membership_number": "...",
  "club_membership_number": "...",
  "customer": {
    "name": {
      "prefix": "Mr",
      "first_name": "Joe",
      "infix": "van der",
      "last_name": "Doe",
      "organization": "TheClub"
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

## Example Request Body

```javascript
{
  "external_invoice_number": "2014-342-545",
  "reference": "ba6fe77",
  "direct_debit_iban": "...",
  "federation_membership_number": "...",
  "club_membership_number": "...",
  "customer": {
    "name": {
      "prefix": "Mr",
      "first_name": "Joe",
      "infix": "van der",
      "last_name": "Doe",
      "organization": "TheClub"
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

## Error Messages

* `invalid_invoice_id`: No invoice with this `invoice_id` could be found.
* `invalid_external_invoice_number`: formatting error: min. 1 character.
* `invalid_customer_last_name`: Last name may not be empty.
* `invalid_customer_email`: Email address may not be empty if no phone number is provided.
* `invalid_customer_phone`: Phone number may not be empty if no email address is provided.
* `invalid_content_type`: `Content-Type: application/json` must be provided.

{% api-method method="post" host="https://api.clubcollect.com/api" path="/v2/invoices/:id/credit\_and\_retract" %}
{% api-method-summary %}
Credit and Retract Invoice
{% endapi-method-summary %}

{% api-method-description %}
Call this method to credit the total outstanding amount of an invoice and retract it in a single HTTP request. Any payment decision made for the invoice will be cancelled. Additional fees that might be due will be credited automatically. It won't be possible to apply more credits to the invoice.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the Invoice to be retracted.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
Must be `application/json`.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Partner API Key.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="show\_retraction\_reason\_to\_customer" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="external\_invoice\_number" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="retraction\_reason" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=true %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "invoice_id": "...",
  "import_id": "...",
  "external_invoice_number": "2014-342-545",
  "reference": "ba6fe77",
  "invoice_number": "123456",
  "direct_debit_iban": "...",
  "federation_membership_number": "...",
  "club_membership_number": "...",
  "customer": {
    "name": {
      "prefix": "Mr",
      "first_name": "Joe",
      "infix": "van der",
      "last_name": "Doe",
      "organization": "TheClub"
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
  "error": "payment_in_progress"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Example Request Body

```javascript
{
  "external_invoice_number": "2014-342-545",
  "description": "Cash payment",
  "retraction_reason": "Paid by cash",
  "show_retraction_reason_to_customer": true
}
```

## Error Messages

* `invalid_invoice_id`: No invoice with this ID could be found.
* `invalid_external_invoice_number`: min. 1 character
* `invalid_description`: `description` must be provided.
* `already_retracted`: The invoice with this ID has already been retracted.
* `invalid_content_type`: `Content-Type: application/json` must be provided.
* `payment_in_progress`: An invoice can't be credited or retracted if there's a payment in progress

{% api-method method="delete" host="https://api.clubcollect.com/api" path="/v2/invoices/:id" %}
{% api-method-summary %}
Delete Invoice
{% endapi-method-summary %}

{% api-method-description %}
Deletes an invoice. Deleting an invoice is possible only when it's not transmitted yet.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
Invoice ID
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
Invoice successfully deleted.
{% endapi-method-response-example-description %}

```text

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
  "error": "invoice_already_transmitted"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

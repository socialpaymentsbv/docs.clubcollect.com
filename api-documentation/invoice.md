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
A Partner usually calls this method in response to a notification sent by ClubCollect about an update to an Invoice.
{% endhint %}


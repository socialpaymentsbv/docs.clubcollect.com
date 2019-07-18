---
description: Manage Invoice Line Items.
---

# Invoice Line

{% api-method method="get" host="https://api.clubcollect.com/api" path="/v2/invoices/:id/lines" %}
{% api-method-summary %}
Fetch Invoice Lines
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of Invoice for which Line Items wish to be retrieved.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
Must be: `application/json`.
{% endapi-method-parameter %}
{% endapi-method-headers %}

{% api-method-query-parameters %}
{% api-method-parameter name="api\_key" type="string" required=true %}
Partner API Key.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Invoice Lines fetched successfully.
{% endapi-method-response-example-description %}

```javascript
{   
  "import_id": "...",   
  "invoice_id": "...",    
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
      "description": null,            
      "date": "...",
      "payment_method": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "CHARGEBACK-LINE",            
      "amount_cents": 123,           
      "description": null,            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",           
      "type": "CHARGEBACK-FEE-LINE",            
      "amount_cents": 123,           
      "description": null,            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "CHARGEBACK-FEE-PAYMENT-LINE",            
      "amount_cents": 123,            
      "description": null,            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "LATE-PAYMENT-FEE-LINE",            
      "amount_cents": 123,            
      "description": null,            
      "date": "..."        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "LATE-PAYMENT-FEE-PAYMENT-LINE",            
      "amount_cents": 123,            
      "description": null,            
      "date": "...",
      "payment_method": "..."        
        
    },        
    {          
      "invoice_line_id": "...",            
      "type": "INSTALLMENT-FEE-LINE",            
      "amount_cents": 123,            
      "description": null,            
      "date": "..."        
      },        
      {          
        "invoice_line_id": "...",            
        "type": "INSTALLMENT-FEE-PAYMENT-LINE",           
        "amount_cents": 123,            
        "description": null,            
        "date": "...",        
        "payment_method": "..."        
        }    
      ],      
    "amount_total_cents": "..."
  }
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Invoice not found.
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
**Note** the date format is`ISO 8601`.
{% endhint %}

{% hint style="info" %}
**Note** that `description` is not `null` only for regular Invoice Lines and Credit Lines.
{% endhint %}

{% hint style="info" %}
**Note** that `payment_method` is present only for Payment Lines and its value can be one of:

- `ideal`
- `sdd`
- `bank_transfer`
- `credit_card`
- `bancontact`
- `bacs`
- `sofort`
- `external`

{% endhint %}

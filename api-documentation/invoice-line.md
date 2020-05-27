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
      "amount_cents": -123,
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
        "amount_cents": -123,
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

* `ideal`
* `sdd`
* `bank_transfer`
* `credit_card`
* `bancontact`
* `bacs`
* `sofort`
* `paypal`
* `external`
{% endhint %}

## Line types

The invoice lines can be of 2 basic types: increasing the invoice balance (regular lines, fees, chargebacks) and will have a positive amount attribute or decreasing the invoice balance (payments, credits) and will have a negative amount attribute. Furthermore lines can be categorized by their type (e.g.: Installment fees, Late payment fees).

The type of an invoice line can be determined by the `type` attributes (always present) and the optional `subtype` attributes.


### Regular Lines

This line type is used for lines added to the invoice at creation time, when increasing the invoice amount
from the ClubCollect web interface or when a member adds a donation to the invoice (if enabled).

| Type | Subtype | Description |
|-|-|-|
| `INVOICE-LINE` | | Regular Invoice line |
| `INVOICE-LINE` | `donation` | Donation Invoice line |
| `INVOICE-LINE` | `surcharge` | Payment process fee Invoice line |

### Fees Lines

At certain points of the life cycle of an invoice fees can be added to the invoice (e.g. Member initiating a payment
in installments).


| Type | Subtype | Description |
|-|-|-|
| `INSTALLMENT-FEE` | | Fee members must pay when paying for an invoice in installments |
| `CHARGEBACK-FEE` | | When a payment is charged back a fee will be added to the invoice |
| `LATE-PAYMENT-FEE` | | Late payment fee added when reminders are sent |

### Payment Lines

When payments are made (either directly by member or external payments added from the Club Collect web interface)
payment invoice lines will are added to the invoice.


| Type | Subtype | Description |
|-|-|-|
| `PAYMENT` | | Payments towards the regular invoice lines |
| `PAYMENT` | `donation` | Payments towards donation invoice lines |
| `JEUGDFONDS` | `jsf` | Jeugdfonds payment |
| `PAYMENT-INSTALLMENT-FEE` | | Payments for installment fees |
| `PAYMENT-CHARGEBACK-FEE` | | Payments for chargeback fees |
| `PAYMENT-LATE-PAYMENT-FEE` | | Payments for late payment fees |
| `PAYMENT-PENALTY-FEE` | | Payment for penalty fees (Legacy) |


## Chargeback Lines

When a previously successful payment is charged back (usually happens for Sepa Direct Direct or Card payments)
Club Collect will generate chargeback lines for the registered payment lines.

| Type | Subtype | Description |
|-|-|-|
| `CHARGEBACK` | | Chargeback line for regular invoice lines |
| `CHARGEBACK` | `donation` | Chargeback line for donation invoice lines |
| `CHARGEBACK-INSTALLMENT-FEE` | | Chargeback for installment fees |
| `CHARGEBACK-LATE-PAYMENT-FEE` | | Chargeback for late payment fee |
| `CHARGEBACK-CHARGEBACK-FEE` | | Chargeback for paid chargeback fees |
| `CHARGEBACK-PENALTY-FEE` | | Chargeback for penalty fees |

## Credit Lines

When credits are added to an invocie or fees are credited from the Club Collect Web Interface we will add
a new invoice line to the invoice.

| Type | Subtype | Description |
|-|-|-|
| `CREDIT-LINE` | | General credit line |
| `CREDIT-LINE` | `donation` | Credit for donation lines |
| `CREDIT-LINE` | `surcharge` | Credits for the payment fee |
| `CREDIT-CHARGEBACK-FEE` | | Credits for a chargeback fee |
| `CREDIT-INSTALLMENT-FEE` | | Credit for an installment fee |
| `CREDIT-LATE-PAYMENT-FEE` | | Credit for a late payment fee |
| `CREDIT-PENALTY-FEE` | | Credit for a Penalty fee |


Note: penalty lines are a legacy types. You'll see this in the API for older invoices but no new invoice lines
with have this type.

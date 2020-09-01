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

The invoice lines can either increase the invoice outstanding \(positive amount\), e.g. regular lines, fees, chargebacks; or decrease the outstanding \(negative amount\), e.g. payments, credits. Furthermore lines can be categorised by their type.

The type of an invoice line is determined by the `type` attributes \(always present\) and the optional `subtype` attributes. Below you can find a description of the possible values for invoice lines types.

### Regular Lines

This line type is used for lines added to the invoice at creation time, when increasing the invoice amount from the ClubCollect web interface or when a member adds a donation to the invoice \(if enabled\).

| Type | Subtype | Description |
| :--- | :--- | :--- |
| `INVOICE-LINE` |  | Amounts added by the partner when an invoice is created will be of this type |
| `INVOICE-LINE` | `donation` | Donation added to an invoice |
| `INVOICE-LINE` | `surcharge` | Payment fee charged to the receiver of the invoice |

### Fees Lines

At certain points of the life cycle of an invoice fees can be added to the invoice \(e.g. Member initiating a payment in installments\).

| Type | Subtype | Description |
| :--- | :--- | :--- |
| `INSTALLMENT-FEE` |  | These fees are added to the invoice when it is paid in installments |
| `CHARGEBACK-FEE` |  | When a payment is charged back a fee might be added to the invoice |
| `LATE-PAYMENT-FEE` |  | Late payment fees are penalties that might be added when the invoice is overdue |

### Payment Lines

Payment lines are added to register new payments happening for an invoice. payment invoice lines will are added to the invoice.

| Type | Subtype | Description |
| :--- | :--- | :--- |
| `PAYMENT` |  | Payment for the amount invoiced by the partner |
| `PAYMENT` | `donation` | Payments towards donation invoice lines |
| `JEUGDFONDS` | `jsf` | Jeugdfonds payment |
| `PAYMENT-INSTALLMENT-FEE` |  | Payments for installment fees |
| `PAYMENT-CHARGEBACK-FEE` |  | Payments for chargeback fees |
| `PAYMENT-LATE-PAYMENT-FEE` |  | Payments for late payment fees |
| `PAYMENT-PENALTY-FEE` |  | Payment for penalty fees \(Legacy\) |

## Chargeback Lines

When a successful payment \(usually Sepa Direct Debit\) is charged back, chargeback lines are added to the invoice to cancel the amount of the payment that has been charged back.

| Type | Subtype | Description |
| :--- | :--- | :--- |
| `CHARGEBACK` |  | Chargeback for the amount invoiced by the partner |
| `CHARGEBACK` | `donation` | Chargeback line for donation invoice lines |
| `CHARGEBACK-INSTALLMENT-FEE` |  | Chargeback for installment fees |
| `CHARGEBACK-LATE-PAYMENT-FEE` |  | Chargeback for late payment fee |
| `CHARGEBACK-CHARGEBACK-FEE` |  | Chargeback for paid chargeback fees |
| `CHARGEBACK-PENALTY-FEE` |  | Chargeback for penalty fees |

## Credit Lines

Credit lines are added to the invoice to discount an amount from the amount outstanding. a new invoice line to the invoice.

| Type | Subtype | Description |
| :--- | :--- | :--- |
| `CREDIT-LINE` |  | Discount applied to the amount invoiced by the partner |
| `CREDIT-LINE` | `donation` | Credit for donation lines |
| `CREDIT-LINE` | `surcharge` | Credits for the payment fee |
| `CREDIT-CHARGEBACK-FEE` |  | Credits for a chargeback fee |
| `CREDIT-INSTALLMENT-FEE` |  | Credit for an installment fee |
| `CREDIT-LATE-PAYMENT-FEE` |  | Credit for a late payment fee |
| `CREDIT-PENALTY-FEE` |  | Credit for a Penalty fee |

Note: penalty lines are a legacy type. You might see some of them for older invoices but no new invoice lines of this type are created. with have this type.


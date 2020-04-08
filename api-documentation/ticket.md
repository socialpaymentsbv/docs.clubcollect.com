# Ticket

{% api-method method="get" host="https://api.clubcollect.com/api" path="/v2/invoices/:id/tickets" %}
{% api-method-summary %}
Fetch Tickets
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of Invoice for which Tickets wish to be fetched.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
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
"tickets": [
  {
   "ticket_id": "...",
   "message": "I don't want to pay",
   "sender": "CUSTOMER",
   "date": "..."
  },
  {
   "ticket_id": "...",
   "message": "Please pay before the 30th",
   "sender": "COMPANY",
   "date": "..."
   }
]
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

{% api-method method="post" host="https://api.clubcollect.com/api" path="/v2/invoices/:id/tickets" %}
{% api-method-summary %}
Create Ticket
{% endapi-method-summary %}

{% api-method-description %}
Create a support Ticket for an Invoice.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID for the Invoice to which the Ticket should be attached.
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
{% api-method-parameter name="message" type="string" required=true %}
Contents of the Ticket.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "ticket_id": "...",
  "message": "Please pay before the 30th",
  "sender": "COMPANY",
  "date": "..."
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

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_message"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.clubcollect.com/api" path="/v2/invoices/:id/tickets/actions/archive" %}
{% api-method-summary %}
Archive Ticket
{% endapi-method-summary %}

{% api-method-description %}
Archive all Tickets for an Invoice.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the Invoice for which Tickets should be archived.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-headers %}
{% api-method-parameter name="Content-Type" type="string" required=true %}
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
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}

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
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://api.clubcollect.com/api" path="/v2/invoices/:id/tickets/actions/assign\_to\_support" %}
{% api-method-summary %}
Assign Ticket to Support
{% endapi-method-summary %}

{% api-method-description %}
Assign Tickets for an Invoice to ClubCollect Support Team.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of Invoice for which Tickets should be assigned to Support.
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
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=204 %}
{% api-method-response-example-description %}

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
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://api.clubcollect.com/api" path="/v2/companies/:id/tickets/:status" %}
{% api-method-summary %}
Fetch All Tickets
{% endapi-method-summary %}

{% api-method-description %}
Returns the list of tickets linked to a company, filtered by Ticket status, paginated and sorted in ascending order, i.e. from oldest to newest.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="status" type="string" required=true %}
One of: `{ unanswered answered archived }`
{% endapi-method-parameter %}

{% api-method-parameter name="id" type="string" required=true %}
ID of Company for which Tickets should be fetched.
{% endapi-method-parameter %}

{% api-method-parameter name="page" type="string" required=false %}
Page requested. If not specified, default to `1`. Page size is `30`.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
"tickets": [
  {
   "invoice_id": "...",
   "ticket_id": "...",
   "message": "I don't want to pay",
   "sender": "CUSTOMER",
   "date": "..."
  },
  {
   "invoice_id": "...",
   "ticket_id": "...",
   "message": "Please pay before the 30th",
   "sender": "COMPANY",
   "date": "..."
   }
]
"page": {
  "page_number": 1,
  "page_size": 12,
  "total_entries": 53,
  "total_pages": 5
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
Company with supplied ID does not exist.
{% endapi-method-response-example-description %}

```javascript
{
  "error": "not_found"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
Supplied status value is invalid.
{% endapi-method-response-example-description %}

```javascript
{
  "error": "invalid_action"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


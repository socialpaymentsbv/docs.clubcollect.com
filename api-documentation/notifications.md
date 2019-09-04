---
description: Receive updates from ClubCollect
---

# Notifications

ClubCollect sends out notifications to Partners regarding changes to Invoices and Import Batches. Notifications are sent out on a regular basis every ten minutes. A Partner must set up an endpoint to receive these notifications via an HTTP POST request containing a JSON body. This endpoint should be communicated to ClubCollect before going live with an integration.

The format of the request body is as follows:

```javascript
{
  "api_key": "7742c368f2dce09b78ddcaf50c61cd238b8e99cb",
  "invoice_ids": [
    "912ebbcef7c775b0d00dc098cd7e213c6dbf8ci3",
    "5ed8b53b56de52e69e946930f233b07db6ee4fbb",
    "34a8e3d65c50d50ac0b8a187dca8301a08266c83"
  ],
  "import_ids": [
    "92bce68ef0e4cc29e9e214f8380316820e081c50"
  ]
}
```

{% hint style="info" %}
The `api_key` is provided in the request body so that you can verify that the request comes from ClubCollect.
{% endhint %}

Using both the `invoice_ids` array and the `import_ids` array allows the Partner to fetch invoices and imports respectively via the relevant API endpoints to pull through the latest information. For example, after receiving the request body from the example above, four API calls could be made to fetch data on three invoices and one import.

This covers all data with regards to an invoice, including notifications of payments, credits, and updates to personal and contact information attached to an invoice.

{% hint style="warning" %}
To avoid overloading the server, requests should be spread out rather than being executed at once.
{% endhint %}


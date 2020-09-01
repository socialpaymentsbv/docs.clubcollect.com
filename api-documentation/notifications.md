---
description: Receive updates from ClubCollect
---

# Notifications

ClubCollect sends out notifications to Partners regarding changes to Invoices and Import Batches. Notifications are sent out on a regular basis every ten minutes.

Notifications are sent as HTTPS callbacks \(webhooks\) to an endpoint on a server managed by the Partner. To receive notifications, the requirements for the server are:

* An endpoint that can accept a JSON payload in an HTTP POST request.
* An open TCP port for HTTPS traffic

This endpoint should be communicated to ClubCollect before going live with the payment integration.

The format of the JSON payload sent in the notifications is as follows:

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

ClubCollect expects a 200 OK as a confirmation of receipt of the notifications. If the Partner's endpoint does not return a 200 OK, ClubCollect will include the notifications that have not been confirmed in the next round of notifications sent.

## Real-time \(synchronous\) Notifications

Besides the notifications that ClubCollect sends asynchronously in groups every ten minutes, which are enabled by default and of mandatory implementation, a Partner may also receive updates synchronously whenever there is an update in a single invoice. This type of notifications are disabled by default and can be enabled upon request to ClubCollect.

Real-time are sent to the same endpoint as the asynchronous notifications. The format of the payload is the same, though for this type of notifications, only one invoice id will be provided per request.

```javascript
{
  "api_key": "7742c368f2dce09b78ddcaf50c61cd238b8e99cb",
  "invoice_ids": [
    "912ebbcef7c775b0d00dc098cd7e213c6dbf8ci3"
  ],
  "import_ids": [ ]
}
```

As in the case of asynchronous notifications, ClubCollect expects a 200 OK as a confirmation of receipt of the notification. If the Partner's endpoint does not return a 200 OK, ClubCollect will not retry to send the notification synchronously, but it will be enqueued to be included in the next round of asynchronous notifications.

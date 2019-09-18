---
description: Use ClubCollect as your payment provider
---

# Payments \(WIP\)

{% api-method method="get" host="https://app.clubcollect.com/api/v2/payments" path="/ideal" %}
{% api-method-summary %}
iDEAL payments
{% endapi-method-summary %}

{% api-method-description %}
This endpoint allows to start a new iDEAL payment and redirects the user to the payment page.

To start the payment session, the partner needs to generate the payment URL with the required parameters and add a signature to avoid tampering with data.

Payments will always be linked to an invoice in ClubCollect. The invoice will be created ad hoc from the parameters received in the request, unless the partner provides an invoice_id to be paid. When the invoice_id is given, the payment will be generated for the total amount due for the invoice.

The invoices that are generated ad hoc are grouped in batches, per month. These batches can be found on
`https://app.clubcollect.com/treasurer/import\_batches\`, named `iDEAL (<year>-<month>)` by default, e.g. `iDEAL (2019-08)`.


##Signature##

To ensure authenticity and data integrity of incoming payment requests ClubCollect requires these requests to be signed. This signature is based on a Hash-based Message Authentication Code (HMAC) calculated using a request's key-value pairs and a secret key, which is known only to the partner and ClubCollect.

Before sending a payment request to ClubCollect, the partner has to calculate the signature and add it as a request parameter. When a request comes in, ClubCollect calculates the same signature based on the received key-value pairs and the secret key. By verifying that both signatures are equal, ClubCollect ensures that the request is not tampered.

Similarly, the partner can validate responses from ClubCollect by calculating the corresponding signature and comparing it with the signature in the response.


Let's explain now how to calculate the signature step by step using the key-value pairs in the table below as example.

Note that code snippets are provided in Ruby.

key | value
--- | ---
`first_name` | `John`
`redirect_url` | `http://partner-test.nl`
`country_code` | `NL`
`external_invoice_number` | `123456`
`amount_cents` | `1000`
`last_name` | `Doe`
`locale` | ``
`company_id` | `d4b8772c67154a6bced8a8b827e177cc00111fe0`
`payment_reference` | `Club membership 2019/2`

partner API key: `3ac2bf2359c1eb184fe0fea01f624bc1d8581981`

1. Discard key-value pairs for which value is null or an empty string

key | value
--- | ---
`first_name` | `John`
`redirect_url` | `http://partner-test.nl`
`country_code` | `NL`
`external_invoice_number` | `123456`
`amount_cents` | `1000`
`last_name` | `Doe`
`company_id` | `d4b8772c67154a6bced8a8b827e177cc00111fe0`
`payment_reference` | `Club membership 2019/2`


2. Sort the key-value pairs by key.

key | value
--- | ---
`amount_cents` | `1000`
`company_id` | `d4b8772c67154a6bced8a8b827e177cc00111fe0`
`country_code` | `NL`
`external_invoice_number` | `123456`
`first_name` | `John`
`last_name` | `Doe`
`payment_reference` | `Club membership 2019/2`
`redirect_url` | `http://partner-test.nl`

3. Concatenate every key-value pair on the list obtained in the previous step to get the signing string

```
signing_string = params.keys.sort.flat_map { |k| [k, params[k]] }.join
```

```
amount_cents1000company_idd4b8772c67154a6bced8a8b827e177cc00111fe0country_codeNLexternal_invoice_number123456first_nameJohnlast_nameDoepayment_referenceClub membership 2019/2redirect_urlhttp://partner-test.nl
```

4. Calculate SHA256 digest of the signing string

```
digested_content = Digest::SHA256.digest(signing_string)
```

```
\tD!()\xAFL\xED\x069\xC0\xEC\x11/\xB3\x93\xFAM\xC0\xA9\xE7\x03\x03\e\xDC\xDFF\x9FZ\x15\xD6\xD1
```

5. Calculate HMAC SHA-256 signature of digested signing string using the API key.

```
hmac_binary = OpenSSL::HMAC.digest(OpenSSL::Digest.new('sha256'), api_key, digested_content)
```

6. Encode the result from binary to hexadecimal
```
signature = hmac_binary.unpack1('H*')
```

The signature calculated for the example key-value pairs and API key is:
```
754966cc8946c8125b365fcb5cf0e27edd98fe7516de7ea17f1b5254bcf7a00e
```

After the signature is generated, it has to be appended to the url query string as
`&signature=754966cc8946c8125b365fcb5cf0e27edd98fe7516de7ea17f1b5254bcf7a00e`

##Payment response##

Once the users finish the payment process, they are redirected to a result page of your choice, included in the payment request as `redirect_url`.

ClubCollect will append parameters to this URL. `payment_result` will inform the partner about the payment status. If the status is already determined (either `authorised` or `refused` or `cancelled`), this information can be used to display a payment successful or payment failed or payment cancelled page.

In a case when the current status is `pending`, the outcome of the payment will be communicated with payment notifications.

The partner is encouraged to store the `invoice_id` and `payment_id` returned in ClubCollect responses and payment notifications, they will be needed to track the status of the payments. As an alternative, the partner can provide a unique `external_invoice_number` parameter in the payment request and ClubCollect will include it on the response and notifications.

The `payment_result` can have one of these values:

* `authorized` - the payment was successfully processed and accepted by the payment provider
* `refused` - the payment could not be processed due to invalid data introduced by the user
* `cancelled` - the payee cancelled the payment or the payment session was ended by the payment provider due to inactivity of the payee.
* `pending` - the payment is submitted for processing but the payment provider hasn't sent yet the result
* `error` - the request was invalid or there was a general error on provider side (payment state is unknown)

##Payment notifications##

For some online payment methods such as iDEAL, the outcome the payment request might take several hours to confirm. As soon as ClubCollect receives any update from the payment provider, a payment notification will be sent to the partner to communicate about the change in the payment status.

Notifications are sent as HTTPS callbacks (webhooks) to an endpoint on your server. To receive notifications, you need a server that has:

* An endpoint that can accept a JSON payload in an HTTP POST request.

* An open TCP port for HTTPS traffic

This endpoint should be communicated to ClubCollect before going live with the payment integration.

The format of the JSON payload sent in the notifications is as follows:

```
{
  "api_key": <secret-partner-api-key>,
  "company_id" => <unique-company-id>,
  "invoice_id" => <unique-invoice-id>,
  "external_invoice_number" => <unique-partner-invoice-number>,
  "payment_id" => <unique-payment-id>,
  "payment_method": "ideal",
  "payment_result": "authorized|cancelled"
}
```

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}

{% api-method-parameter name="company_id" type="string" required=true %}
Unique identifier of the company receiver of the payment.
{% endapi-method-parameter %}

{% api-method-parameter name="redirect_url" type="string" required=true %}
When payee completes or canceles the payment process, the request will be redirected to this URL. ClubCollect will append some additional
parameters to the request which will allow the partner to know the current state of the payment. See below in the response section.
{% endapi-method-parameter %}

{% api-method-parameter name="signature" type="string" required=true %}
Request signature
{% endapi-method-parameter %}

{% api-method-parameter name="invoice_id" type="string" required=false %}
ID of an invoice that has been already generated by the partner for the payee. In case it's provided, the payment generated
will be for the total amount due for the given invoice. This can be used by the partner when the payee starts the
payment process and the payment is left incomplete or it's cancelled.

In case invoice_id  is given, amount_cents, last_name and the rest of parameters below will be ignored. These are used
 only to generate a new invoice.
{% endapi-method-parameter %}

{% api-method-parameter name="last_name" type="string" required=true %}
Last name of the payee. Required unless invoice_id is provided.
{% endapi-method-parameter %}

{% api-method-parameter name="amount_cents" type="integer" required=true %}
Amount in cents that is going to be paid. Required unless invoice_id is provided.
{% endapi-method-parameter %}

{% api-method-parameter name="payment_reference" type="string" required=false %}
Reference of the payment, will be used as description of the invoice line. {% endapi-method-parameter %}
{% api-method-parameter name="first_name" type="string" required=false %} First name of the payee. {% endapi-method-parameter %}

{% api-method-parameter name="external_invoice_number" type="string" required=false %}
{% endapi-method-parameter %}

{% api-method-parameter name="locale" type="string" required=false %}
Language that will be used in the payment process. If not given, the company default locale will be used.
{% endapi-method-parameter %}

{% api-method-parameter name="first_name" type="string" required=false %}
  First name of the payee.
{% endapi-method-parameter %}

{% api-method-parameter name="prefix" type="string" required=false %}
  Prefix of the name of the payee.
{% endapi-method-parameter %}

{% api-method-parameter name="infix" type="string" required=false %}
  Prefix of the name of the payee.
{% endapi-method-parameter %}

{% api-method-parameter name="address1" type="string" required=false %}
  Payee street name
{% endapi-method-parameter %}

{% api-method-parameter name="house_number" type="string" required=false %}
  Payee address number
{% endapi-method-parameter %}

{% api-method-parameter name="zipcode" type="string" required=false %}
  Payee ZIP code. If it's given, it must be less than 16 characters.
{% endapi-method-parameter %}

{% api-method-parameter name="city" type="string" required=false %}
  Payee city. If it's given, it must be less than 35 characters.
{% endapi-method-parameter %}

{% api-method-parameter name="email_address" type="string" required=false %}
  Payee email address.
{% endapi-method-parameter %}

{% api-method-parameter name="phone_number" type="string" required=false %}
  Payee phone number.
{% endapi-method-parameter %}

{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}
The payment request is valid, the payee is redirected to the payment page and completes the payment process.
The user will be redirected to the `redirect_url` specified by the partner in the payment request and the parameters listed below will be appended to the URL. ClubCollect will add also a signature to the request, only considering the parameters added to the request by ClubCollect.
{% endapi-method-response-example-description %}
{
    "company_id": "25b39de9bedc3409e195a99bb3a31918c12182e7",
    "invoice_id": "e06be9959a6d5ad6e1ce80caf97e3244d6024dd1",
    "payment_id": "ae515fabdd886cd0c49408f9696c5498848977fe",
    "payment_method": "ideal",
    "payment_result": "authorized",
    "external_invoice_number": "12345",
}
{% endapi-method-response-example %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}
The payment request is valid, the payee is redirected to the payment page and completes the payment but the payment provider wasn't able to authorize the payment yet.
{% endapi-method-response-example-description %}

{
    "company_id": "25b39de9bedc3409e195a99bb3a31918c12182e7",
    "invoice_id": "e06be9959a6d5ad6e1ce80caf97e3244d6024dd1",
    "payment_id": "ae515fabdd886cd0c49408f9696c5498848977fe",
    "payment_method": "ideal",
    "payment_result": "pending",
    "external_invoice_number": "12345",
}
{% endapi-method-response-example %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}
The payment request is valid, the payee is redirected to the payment page but the payment is cancelled
by the payee.

{% endapi-method-response-example-description %}
{
    "company_id": "25b39de9bedc3409e195a99bb3a31918c12182e7",
    "invoice_id": "e06be9959a6d5ad6e1ce80caf97e3244d6024dd1",
    "payment_id": "ae515fabdd886cd0c49408f9696c5498848977fe",
    "payment_method": "ideal",
    "payment_result": "cancelled",
    "external_invoice_number": "12345",
}
{% endapi-method-response-example %}

{% api-method-response-example httpCode=302 %}
{% api-method-response-example-description %}
The payment request has an invalid signature
{% endapi-method-response-example-description %}

{
    "company_id": "25b39de9bedc3409e195a99bb3a31918c12182e7",
    "payment_method": "ideal",
    "error_code": "unprocessable_entity",
    "error_details": "invalid_signature;invalid_partner"
}
{% endapi-method-response-example %}

{% endapi-method-response %}

{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://app.clubcollect.com/api/v2/payments" path="/:payment_id" %}
{% api-method-summary %}
Check status of a payment
{% endapi-method-summary %}

{% api-method-description %}
ClubCollect will inform about any changes in the status using payment notifications. This endpoint can be used as a "backup" by the partner to check the current status of a payment in case any notification is dismissed.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}

{% api-method-parameter name="payment_id" type="string" required=true %}
  Unique payment identifier returned by ClubCollect in the payment response.
{% endapi-method-parameter %}

{% api-method-parameter name="company_id" type="string" required=true %}
Unique identifier of the company receiver of the payment.
{% endapi-method-parameter %}

{% api-method-parameter name="signature" type="string" required=true %}
Request signature.
{% endapi-method-parameter %}

{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}

{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
When all the parameters are valid, the endpoint will return a JSON payload informing about the current status of the payment similar to the payload in the payment notifications.
{% endapi-method-response-example-description %}
{
    "company_id": "25b39de9bedc3409e195a99bb3a31918c12182e7",
    "invoice_id": "e06be9959a6d5ad6e1ce80caf97e3244d6024dd1",
    "payment_id": "ae515fabdd886cd0c49408f9696c5498848977fe",
    "payment_method": "ideal",
    "payment_result": "authorized",
    "external_invoice_number": "12345",
    "created_at": "2019-09-15T16:15:56Z",
    "updated_at": "2019-09-15T16:38:07Z",
}
{% endapi-method-response-example %}

{% api-method-response-example httpCode=422 %}
{% api-method-response-example-description %}
When one of the parameters is invalid, the JSON payload will inform about the error.
{% endapi-method-response-example-description %}
{
    "company_id": "25b39de9bedc3409e195a99bb3a31918c12182e7",
    "error_code": "invalid_params",
    "error_details": "invalid_payment_id"
}
{% endapi-method-response-example %}
{% endapi-method-response %}

{% endapi-method-spec %}
{% endapi-method %}

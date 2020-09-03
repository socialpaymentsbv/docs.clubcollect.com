---
description: A guide to integration for Partners.
---

# Partner Integration

The following describes a typical integration in a step-by-step fashion, assuming a desire to invoice on behalf of an organisation \(known as **Company**\) from start to finish.

## Preface: Partner Credentials

In dialogue with ClubCollect a Partner Account will be set up and a **token** issued \(referred to in the documentation as an `api_key`\). This token is to be used to authenticate requests against the ClubCollect API. 

{% hint style="danger" %}
This is your unique token identifying requests. **It must be protected at all times.** Should you believe your token has been compromised please contact ClubCollect immediately via `support@clubcollect.com`.
{% endhint %}

{% hint style="warning" %}
Authentication passing api_key in the request params is deprecated and it's scheduled to be discontinued.

Partners are encourage to integrate the new authentication scheme, using HTTP authorization header.

```
Authorization: ApiKey <api_key>
```
{% endhint %}

### Data Hierarchy

The following list gives an overview of the data hierarchy:

* Partner
  * Company
    * Import
      * Invoice
        * Invoice Line
        * Ticket

In other words:

* a **Partner** can have one or many **Companies**
* a **Company** can have one or many **Imports**
* an **Import** contains one or many **Invoices**
* an **Invoice** can have:
  *  one or many **Invoice Lines**
  * one or many **Tickets**

## 1. Create Company

For each individual organisation that you represent as an entity wishing to engage the ClubCollect Service a **Company** record must be created. This is an umbrella that scopes activity to that particular organisation. This is usually equivalent to a legal entity, such as a sports club, member organisation or company which are likely registered with the local Chamber of Commerce.

To create a Company, please see the [_Company API Documentation_](../api-documentation/company.md).

## 2. Create an Empty Import

An **Import** acts as a holding place for a collection of one or more Invoices. It is designed so that Invoices which require the same configuration \(e.g. message flow, payment options\) can be grouped together. Each Import can have different settings applied, but Invoices in the same Import will all have the same configuration

To create an Import, please see the [_Import API Documentation_](../api-documentation/import.md#create-import). 

## 3. Add Invoice\(s\) to the Import

**Invoices** can be added to the Import for as long as the Import remains “open”. The cut-off point is when an Import is transmitted \(or sent\) after which the Import is “closed“. Invoices must contain at least one Invoice Line and that Invoice Line must be zero or negative. Invoices are created one-by-one, there is no way to create multiple Invoices in one request.

To create Invoice\(s\), please see the [_Invoice API Documentation_](../api-documentation/invoice.md#create-invoice).

## 4. Redirect to ClubCollect.com

When an Import contains all of the relevant Invoices it is time to transmit the Invoices, which is the point at which the ClubCollect Service kicks in.

Before transmission there is opportunity to review the configuration that will be applied to the Import and to update relevant settings. Due to the complexity involved in these settings \(read more about [_Invoice Settings_](../overviews/clubcollect-service.md#invoice-settings)\) we require treasurers to use the ClubCollect.com user interface to configure the Import appropriately and then transmit the Import.

A Partner can expose a Single Sign On \(SSO\) link in their product that will redirect a user to the relevant Import page on ClubCollect.com where the user can apply the configuration and transmit the batch.

## 5. Receive Invoice Notifications

When an Import has been transmitted and the communication has gone out to Invoice recipients then payments will start coming in. In order to notify partners about events related to the Invoices we send regular notifications. 

With the information provided in the notification it will be possible to query the API to receive the full details of the event\(s\) in question. It is up to the partner to decide whether to reflect changes in the partner system or to rely on the ClubCollect Service as the source of all information.

More information about Notifications will be added to the API Documentation in due course.

## Appendix: Invoice Actions

### A. Credit an Invoice

Please see the [_Invoice API Documentation_](../api-documentation/invoice.md#credit-invoice).

### B. Credit and Retract an Invoice

This is equivalent to the issuing of a Credit Note for the remaining amount outstanding on an Invoice.

Please see the [_Invoice API Documentation_](../api-documentation/invoice.md#credit-and-retract-invoice).


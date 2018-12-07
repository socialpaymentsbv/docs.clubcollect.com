---
description: An overview of the ClubCollect service for Partners.
---

# ClubCollect Service

ClubCollect provides a fully-featured service for the collection of invoices, managing the process from start to finish. A typical example consists of a sports club wanting to collect their annual contributions from members. Other examples include a Small to Medium Enterprise \(SME\) invoicing customers, being used to handle the back office activities of a debt collection agency, or being used for a larger companies debtor department.

## Overview of Service

This can be explained in a high-level overview of the steps involved:

### 1. Importing Invoice Data

Invoices are imported into the system via an Excel sheet or via the API. This consists of all the information necessary to make up an invoice, including the line items.

### 2. Configuring Collection Settings

These are collected into an _Import Batch_ which can then be configured with settings which regulate, among other things, preferred modes of communication and collection. \(See _**Invoice Settings**_ below\)

### 3. Transmitting the Invoices

An Import Batch is then _transmitted_ to effectively begin the collection process as configured in _**Step 2**_, initiating the communication to the individuals whose invoices are due.

### 4. Communication

A typical configuration will send out a maximum of two requests in up to three communication channels:

* Email
* SMS
* Letter

### 5. Response to Communication

An individual will respond to these requests by following a link to a _Member Invoice Page_ which provides opportunity to:

* update contact details
* raise a ticket with the Treasurer concerning the invoice
* view the invoice details \(inc. PDF download\)
* make a payment decision, either
* paying immediately \(e.g. iDEAL\)
* embarking on a payment schedule \(e.g. SEPA Direct Debit\)

See _**Invoice Settings &gt; Payments**_ below for full details of payment options.

### 6. Non-Response

Should an individual not respond to the payment request\(s\), up to three payment reminders can be sent across some or all of the aforementioned communication channels.

### 7. Collection Management

The Treasurer or Administrator has access to a rich, comprehensive toolwhich provides a full overview of the state of the collections process. This includes, but is not limited to:

* see high-level details and totals of all invoices in the system
* details of communications and responses \(or lack thereof\)
* details of payment schedules
* current invoice balances
* details of payments inc. status
* details of payouts to organisation
* ability to view and respond to tickets

Most tables are searchable and filterable to enable quick and easy access to necessary information.

### 8. Payouts

The payments from individuals across all payment methods are received by a third-party escrow account, which transfers the money to organisations on a weekly basis. Reports are available with a full breakdown of items to aid the reconciliation process.

### 9. Non-Collection

For unsuccessful attempts at collection, i.e. after the provisions in _**Step 6**_ have been exhausted, there are means provided to manually trigger additional communication—in bulk if necessary—across all channels. ClubCollect can even call members at a fee. For options where a mandate has been provided we can charge the bank account via Sepa Direct Debit. In the last instance ClubCollect offers the possibility of sending an official last reminder by letter \(e.g. WIK Letter\) and ClubCollect can prepare a log in order to pass on to a debt collection agency.

### 10. Defaulting on a Payment Schedule

For instances where there has been a response, and a payment schedule has been entered into, but the schedule has not been adhered to, e.g. a chargeback occurs on a SEPA Direct Debit payment, or a promise to pay by Bank Transfer has not been fulfilled, then the system is able to react appropriately, sending communications, distributing the principal across remaining installments, and/or creating a fresh opportunity to pay. Visibility for the Treasurer is afforded through the dashboard detailed in _**Step 7**_.

This is one of the areas which provides significant value for treasurers, providing automation for one of the most difficult and time-consuming tasks—chasing up on non-payment—and is only possible in a system like ClubCollect.

For more about payments see _**Invoice Settings &gt; Payments**_ below.

## Invoice Settings

The following settings are available to Treasurers and can be configured per _Batch_ \(or group\) separately. It divides roughly into two sections, Payments and Communication:

### Payments

A Treasurer has the option of offering the choice of several payment options to members, some of which come with additional options. These are explained below:

* iDEAL \(Dutch online bank transfer\)
  * in a one-off payment for the full amount
* SEPA Direct Debit
  * across a schedule of installments that are configurable \(see below\)
  * for organisations who have a mandate from their members and who wish to collect the full amount immediately after the due date in one transaction
* Bank Transfer
  * in a one-off payment for the full amount
  * across a schedule of installments that are configurable \(see below\)
* Credit Card
  * in a one-off payment for the full amount
* Bancontact Card \(Belgium\)
  * in a one-off payment for the full amount
* Bacs Direct Debit \(UK\)
  * in a one-off payment for the full amount

A schedule of payment in installments can be configured for both SEPA Direct Debit and Bank Transfer with the following options:

* Number of installments \(2–12\)
* Interval between installments, in days \(14,21,30,45,60,90,120,150,180\)

The following payment methods are currently in development:

* Sofort \(Germany\)
* Bacs Direct Debit \(UK\)
  * across a schedule of installments that are configurable

ClubCollect currently supports EUR and GBP for receiving money and paying out. Depending on the individual payment method funds could technically be paid in other currencies, e.g. a foreign credit card.

### Communication

Communication occurs across three channels, reaching across the globe:

* Email
* SMS
* Letter

The system will always send emails \(assuming an email address is present\) while SMS and Letter can be toggled on or off for certain messages.

Communication happens with a standard set of well-tested messages, some of these are standard \(indicated with an asterisk \*\), and others are optional:

* Payment Request 1\*
* Payment Request 2
* Payment Reminder 1\*
* Payment Reminder 2\*
* Payment Reminder 3

In the case that you are collecting payment via SEPA Direct Debit in one fell swoop, there are no requests or reminders necessary.

### Pre-financing

ClubCollect offers two flavours of pre-financing, i.e. providing organisations with money before the money has been collected from the members. This must be done in communication with ClubCollect for compliance reasons:

* Pre-financing a lump sum at the beginning of the collection process
* Pre-financing invoices on an individual basis when an individual commits to a payment schedule

In each case ClubCollect pays the organisation up front and then collects the debt from member contributions.

### Other

In addition to the main categories, there are a few other settings that can be configured:

* A Late Payment Fee, if members do not take heed to warnings in requests or reminders the system can add a fee for late payment.
* A personal note, for a custom message from the organisation
* A custom salutation, to be used on each message  

## FAQ

**Why do you use an escrow to process the money?**

This is industry standard practice to ensure the integrity of the relationship. It ensures that ClubCollect, the company, never touches any individual’s money.

**What do members in their bank statement?**

Members will see the name of the escrow account with the organisation name and an invoice reference in the description.

**When do we collect our own fees?**

ClubCollect collects fees on a weekly basis \(to mirror the payout process\).

**Do we net this with the payout or keep this separate?**

Collecting fees is always separate from the payouts.

**Why do we pay out on a weekly basis?**

It has been our experience with organisations that if we payout more often it creates extra administrative work, and if we payout less often then it takes too long for organisations to see their money.


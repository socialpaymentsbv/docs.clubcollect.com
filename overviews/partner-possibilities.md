---
description: An overview of potential integration options for partners.
---

# Partner Possibilities

ClubCollect is excited to partner with organisations to offer the benefits of the ClubCollect service to a wider audience, providing a valuable and attractive addition to your client offering.

### Overview

The goal for us is to provide partners with access to the full range of service that ClubCollect offers in the area of invoice collections. A partner will have information about a number of fees or invoices that need to be collected. An integration then entails:

1. Informing ClubCollect about these invoices from a partner system,
2. Triggering the initiation of the collection process, and
3. Receiving invoice updates from ClubCollect, e.g. payment, in order to update the partner system

The levels of integration may vary, depending on what is desired by the partner, but the above is fairly typical. All of the above happens via the ClubCollect API, see details at the end of this document.

### Potential Integration Options

An integration involves sending information through to ClubCollect and receiving information back from ClubCollect. How involved this becomes depends on the level of integration. The means will be outlined below, followed by a discussion of different integration levels.

#### 1. Options for providing ClubCollect with Invoice Data

1. Pushing invoice data to ClubCollect via the API \(details at end of document\)
2. Exposing an endpoint for ClubCollect to pull invoice data from partner \(experimental\)

#### 2. Options for getting updates from ClubCollect

1. Pulling invoice data via the API \(polling, pull\)
2. Receiving notifications from ClubCollect \(notifications, push\)
3. Manually downloading standard MT940 export file and uploading in partner system \(manual, push\)

_Each of the options for 1. can be paired with each of the options for 2., e.g. 1A+2A, or 1B+1C._

**Integration Levels**

The level of integration required depends largely on what you as the partner would like. A full integration allows the ClubCollect system to remain relatively anonymous but the burden of integration that allows presenting information to the member, having fetched it from ClubCollect, while keeping it in sync, falls to the partner.

A low-touch integration would allow the partner to provide, and essentially “hand-off” invoice data to ClubCollect, and allow the client to use the fully featured ClubCollect dashboard to manage the collection process alongside the partner system rather than in it. There would be no necessity of reporting back to the partner system since the management of the collection process would be completely outsourced.

A middle path allows a variation of the two, e.g. pushing invoice data to ClubCollect, but relying on an MT940 file to receive definitive updates.

### ClubCollect API

API documentation is available on this site. While this provides valuable information about the individual API calls, it does not provide a cohesive overview of the flow necessary to complete a full integration. The following is an attempt to provide that overview.

#### Key Terms

A _**Company**_ is an independent entity that acts as the umbrella for a group of individuals for which collections will be made. Think a sports club, a member organisation or other. It represents the entity that will receive the collections and normally mirrors such a group in the real world. For a partner with multiple organisations as clients there would typically be a Company per client. This corresponds with the `/api/v2/companies` endpoint.

An _**Import**_ belongs to a company and acts as a container for a group of invoices that wish to be transmittedwith the same settings. You would normally create an import for a company, add a collection of invoices \(See Invoice below\) then transmit the import. This corresponds with the `/api/v2/imports` endpoint.

An _**Invoice**_ represents an invoice and is added to an **Import**. It usually contains a number of line items \(see Invoice Lines below\). An invoice can be credited or retracted after transmission. This corresponds with the `/api/v2/invoices` endpoint.

_**Invoice Lines**_ are individual line items on an invoice. This corresponds with the `/api/v2/invoice/{invoice_id}/invoice_lines` endpoint.

Updates to invoices that occur through the collection process are sent to the partner via notifications and, if necessary, further details can be fetched from the API on an individual basis.

#### Flow for Full Integration using API

1. A company needs to be registered with ClubCollect, via the ClubCollect support teamand, in order to collect funds, must be verified \(see Verification below\)._There are plans to allow the creation of a company via the API._
2. Given a company has been verified, indicating that it is ready to collect funds, an import batch can be created via the API. This is a container for a group of invoices.
3. The invoices themselves can be created via the API, complete with their invoice lines.
4. When invoices are ready to be sent, the batch can be transmitted via the API, this kicks off the collection process.
5. Notifications about changes to invoices are sent from via notifications from ClubCollect to the partner, e.g., payment, partial payment, contact detail change etc.
6. Data about invoices/lines etc. can be fetched by the partner via the API at any time
7. Further actions, such as crediting or retracting can be triggered by the partner via the API

#### Flow for Lowest Touch Integration \(without API\)

1. Partner exposes an endpoint allowing ClubCollect to fetch invoice data
2. Partner’s client logs into ClubCollect, adds partner API credentials.
3. ClubCollect fetches invoice data from partner.
4. Partner’s client manages everything via ClubCollect.

**Verification**

In order to be compliant with regulations, we are required to know whether the treasurer/administrator is a legitimate representative of an official organization.

Therefore, we expect the following documents before we can start processing invoices:

* Personal identification documents of organization signatories
* Bank statement of the organization \(with at least IBAN, address and name of the account holder\)
* SEPA mandate
* Proof of registry in the local Chamber of Commerce \(we often download this ourselves\)


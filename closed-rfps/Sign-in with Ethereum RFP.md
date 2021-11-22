# Sign-in with ethereum RFP

## Introduction

The Ethereum Foundation (EF) and True Names LTD (ENS) would like to announce a Request for Proposals (RFP) for the creation of a Sign-In with Ethereum specification, a package using Oauth for easy implementation by web2 services, and a Javascript library for the user-facing part of sign-in.

* [Sign-in with Ethereum RFP](https://notes.ethereum.org/@djrtwo/sign-in-with-ethereum-RFP#Sign-in-with-Ethereum-RFP)
  * [Introduction](https://notes.ethereum.org/@djrtwo/sign-in-with-ethereum-RFP#Introduction)
  * [Scope](https://notes.ethereum.org/@djrtwo/sign-in-with-ethereum-RFP#Scope)
  * [Process Summary](https://notes.ethereum.org/@djrtwo/sign-in-with-ethereum-RFP#Process-summary)
  * [Fee structure](https://notes.ethereum.org/@djrtwo/sign-in-with-ethereum-RFP#Fee-structure)
    * [Invoices](https://notes.ethereum.org/@djrtwo/sign-in-with-ethereum-RFP#Invoices)
    * [Payment method](https://notes.ethereum.org/@djrtwo/sign-in-with-ethereum-RFP#Payment-method)
   * [Bidding instructions](https://notes.ethereum.org/@djrtwo/sign-in-with-ethereum-RFP#Bidding-instructions)


## Scope

* **Survey current practices:** Examine existing uses of Sign-In with Ethereum, look at the code, and talk to the developers. Determine what developers are doing and why, how it could be improved, and what best practices have already emerged.

* **Specification:** Write a specification for how Sign-In with Ethereum should work, both with and without Oauth. Include best practices and recommended graphics. The specification should be simple and generally follow existing practices. Avoid feature bloat, particularly the inclusion of lesser-used projects who see getting into the specification as a means of gaining adoption. The core specification should be decentralized, open, non-proprietary, and have long-term viability. It should have no dependence on a centralized server except for the servers already being run by the application that the user is signing in to. The basic specification should include: Ethereum accounts used for authentication, ENS names for usernames (via reverse resolution), and data from the ENS name’s text records for additional profile information (e.g. avatar, social media handles, etc).

* **Oauth implementation:**  Create an Oauth implementation that makes it easy for services to add Sign-In with Ethereum to their existing sign-in options. This can be the refinement of an existing implementation (e.g. Pelith’s Eauth project) based on the specification, or can be created from scratch.

* **Javascript library:** Create a Javascript library for the user-facing part of the sign-in process. This should be able to be used with or without the Oauth implementation.

## Process summary

The entire process can be summarised as follows:

1. **Request:** Release of RFP (this post)
2. **Gather:** Vendors submit proposals
3. **Deliberate:** EF and ENS decide which proposal(s) to accept, and come up with a plan based on the resources and needs of the accepted proposal(s)
4. **Propose:** EF proposes the plan to vendor, and makes adjustments based on vendor’s feedback
5. **Begin:** Vendor accepts and work begins
6. **Work:** Vendor works on the tasks, in communication with EF and ENS as necessary, and seeking public feedback as appropriate
7. **Finish:** Work is complete, final payments are made
8. **Maintenance:** EF and ENS put in place a plan for ongoing maintenance and development of the specification, Oauth package, and Javascript library

## Fee structure

### Invoices

Based on the timeline of this engagement, the chosen vendor(s) will be expected to submit two invoices:

* a first invoice of 40% of the total engagement fee at the start of the engagement
* a second invoice of 60% of the total engagement fee at the end of the engagement, following the delivery of the final product and a 5 day review period.

### Payment method

The vendor will be given the option to be paid in fiat money (via bank transfer) or ETH.

If the vendor chooses to be paid in ETH, the value of ETH described under the agreement will be the value in USD at NYSE closing time (4 PM EST) on the day prior to the due date (as described at (https://www.coingecko.com)[https://www.coingecko.com])

## Bidding instructions

Upon reception of this request, interested vendors are expected to confirm receipt and intention to bid on the engagement.

In this confirmation, they should explain what they need from us in order to get started. As well as bring attention to areas in which they feel they do not have significant expertise. We will use this information to try to provide appropriate entrance material for the engagement.

Proposals must be submitted before July 30th, 2021 at 5pm PST*. We expect to take up to 2 weeks to deliberate and respond.

Please send initial confirmations, and proposals (in PDF format) to the following address: rfp@ethereum.org

Feel free to send us any questions you may have: rfp@ethereum.org

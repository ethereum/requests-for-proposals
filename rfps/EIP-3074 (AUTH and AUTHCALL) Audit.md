# EIP-3074 (AUTH and AUTHCALL) Audit

## Introduction

The [Ethereum Foundation](https://ethereum.foundation/) (EF) and [Quilt](https://quilt.link/) (Q) would like to announce a Request for Proposals (RfP) for a security review of [EIP-3074: AUTH and AUTHCALL opcodes](https://eips.ethereum.org/EIPS/eip-3074).

[EIP-3074](https://eips.ethereum.org/EIPS/eip-3074) introduces a mechanism in the EVM that can make subcalls as a certain `CALLER`. The `CALLER` is derived from a signature included on-chain. This mechanism has widespread use cases, including sponsored transactions, batched transactions, non-sequential transactions, and more.

However, this EIP changes the existing security properties of the network. Because `CALLER` is the defacto authentication mechanism on-chain, a mechanism that allows contracts to masquerade as EOAs could introduce new threats. The goal of this audit is to uncover and investigate these threats.

## Table of Contents



- EIP-3074 (AUTH and AUTHCALL) Audit
  - [Introduction](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Introduction)
  - [Table of Contents](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Table-of-Contents)
  - [Version of Code for Audit](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Version-of-Code-for-Audit)
  - [Scope of Audit](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Scope-of-Audit)
  - Specific Areas of Focus
    - [Wallet Integration](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Wallet-Integration)
    - [Potential Invoker Bugs](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Potential-Invoker-Bugs)
    - [Existing Smart Contracts](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Existing-Smart-Contracts)
    - [Sponsor-Sponsee Relationship](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Sponsor-Sponsee-Relationship)
  - [Process summary](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Process-summary)
  - [Engagement timeline](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Engagement-timeline)
  - [Deliverables](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Deliverables)
  - Fee Structure
    - [Invoices](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Invoices)
    - [Payment method](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Payment-method)
  - [Selection criteria](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Selection-criteria)
  - [Bidding instructions](https://notes.ethereum.org/@djrtwo/eip-3074-audit-rfp#Bidding-instructions)



## Version of Code for Audit

The git commit of the specification for audit is will be decided near the start of the audit. For now, refer to the latest information contained in the [core EIP](https://eips.ethereum.org/EIPS/eip-3074).

## Scope of Audit

EIP-3074 offers a flexible primitive to develop novel wallet extensions, however, this flexibility increases the surface area of unintended consequences it may have for users and existing applications.

The audit should thoroughly review the EIP specification and explore all potential security concerns discovered, but should primarily focus on the security of user assets, new threat models for users and their wallets, and the feasibility of writing secure invoker contracts.

The analysis of the safety of the network itself (ex. denial of service attacks) is explicitly not in scope. Economic modeling of sponsored transactions is also not in scope.

## Specific Areas of Focus

The following areas are highlighted as particular areas of concern or sensitivity.

### Wallet Integration

Signing a single malicious `AUTH` message would be enough for an adversary to gain full control over an EOA. It should be determined if a wallet can be reasonably expected to protect users from this.

### Potential Invoker Bugs

The EIP strongly recommends users interact only with trusted invokers that have undergone rigorous audits and static analysis. That said, it is still possible for a bug to be discovered in these trusted contracts. This would mean that any EOA that has interacted with the invoker in the past could be at risk. The possibility and range of severities for these bugs in heavily audited invoker contract should be discussed.

### Existing Smart Contracts

Currently, it is possible to determine if a smart contract is executing in the first frame of a transaction by checking that `CALLER == ORIGIN`. This EIP allows the transaction’s originator to set itself as the `CALLER` at any call depth, therefore breaking the aforementioned assumption. It should be determined how contracts use the above check and if existing contracts rely on this assumption, how they would break when the assumption is invalidated.

### Sponsor-Sponsee Relationship

This relationship is hinted at in the EIP, but not thoroughly discussed because it is orthogonal to the actual specification. However, the design of the EIP is highly motivated by the relationship between sponsor and sponsee. Therefore, an audit of the EIP should examine how the two parties will interact.

Specifically, it should be possible, using primitives provided by the EIP, to build a system enabling sponsored transactions, while preventing situations where:

- The sponsor receives payment from the sponsee, but the sponsee’s intended action is not executed.
- The sponsee is able to perform an action, but does not reimburse the sponsor.
- The sponsee is able to repeatedly waste sponsor resources (ex. gas fees, nonces, etc), without incurring a proportional cost itself.

## Process summary

The entire process can be summarized as follows:

1. **Request:** EF releases RfP (this post)
2. **Gather:** Vendors submit proposals
3. **Deliberate:** EF and Q decides which proposal to accept, and comes up with a plan based on the resources and needs of the accepted proposal.
4. **Propose:** EF and Q proposes the plan to vendor, and makes adjustments based on vendor’s feedback
5. **Begin:** Vendor accepts and work begins

## Engagement timeline

The proposed timeline of the engagement is approximately 1 month.

The engagement is broken up into the following stages: a vendor assessment, followed by a break for developer response and mitigation, followed by a review phase from the vendor.

The vendor will then summarize findings and publish the results to help the community understand the work that was done.

| Stage |         Description          |
| :---- | :--------------------------: |
| 1     |   Vendor assessment period   |
| 2     |   Developer issue response   |
| 3     | Vendor review issue response |
| 4     |  Vendor summarises findings  |

Members of the EF and Q will be available at all times to answer questions and comments during the assessment period in order to make life as easy as possible for the vendor.

## Deliverables

The vendor will provide a report summarising the audit findings, distilling the lessons learnt, and an outline of each security issue discovered.

## Fee Structure

### Invoices

Based on the timeline of this audit, the chosen vendor will be expected to submit 2 invoices:

- a first invoice of 40% of the total engagement fee at the start of the engagement
- a second invoice of 60% of the total engagement fee at the end of the engagement, following the delivery of the summary report and a 5 day review period.

### Payment method

The vendor will be given the option to be paid in Fiat money (via bank transfer) or ETH.

If the vendor chooses to be paid in ETH, the value of ETH described under the agreement will be the value in USD at NYSE closing time (4 PM EST) on the day prior to the due date (as described at [https://www.coingecko.com](https://www.coingecko.com/)).

## Selection criteria

The selected vendor will have significant expertise in the areas necessary to meet the needs and requirements set forth in this RfP. Particularly:

```
Familiarity with the EVM, common smart contract techniques
Familiarity with cryptocurrency key management and wallets
High level understanding of meta-transaction relayer architectures
```

The EF and Q have considerable expertise in these domains and are ready to support the vendor.

## Bidding instructions

Upon reception of this request, interested vendors are expected to confirm receipt and intention to bid on the engagement.

In this confirmation, they should explain what they need from us in order to get started. As well as bring attention to areas in which they feel they do not have significant expertise. We will use this information to try to provide appropriate entrance material for the engagement.

Proposals must be submitted before April 18, 2021. We expect to take 1 week to deliberate and respond.

Please send initial confirmations, and proposals (in PDF format) to the following address: [rfp@ethereum.org](mailto:rfp@ethereum.org)

*Feel free to send us any questions you may have: [rfp@ethereum.org](mailto:rfp@ethereum.org)*
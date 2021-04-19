# State Expiry: Request for Proposals

## Introduction

The Ethereum Foundation would like to announce a Request for Proposals (RfP) for the research and development needed to take the proposed concept for "State Expiry" from it's current form into a complete specification and client implementation.

State Expiry is a proposed scheme for introducing economic bounds on the total state size necessary to operate a node on the Ethereum network. The current proposed scheme is currently described in this post from the Ethereum Research forum: https://ethresear.ch/t/resurrection-conflict-minimized-state-bounding-take-2/8739

This proposal has two primary goals.

- Expand the proposed scheme into a complete specification
- Implement it in one of the mainnet Ethereum client codebases. (Besu, Geth, Nethermind, OpenEthereum, TurboGeth)

## Scope

Create an implementation of the epoch based state expiry scheme in one of the mainnet ethereum clients and an accompanying specification in the form of one or more EIPs.  The implementation should be suitable for running a test network.  The EIPs should fully specify all changes necessary for the core consensus protocol.

    
## Process Summary

The entire process can be summarized as follows:

- **Request**: EF releases RfP (this post)
- **Gather**: Vendors submit proposals
- **Deliberate**: EF decides which proposal to accept, and comes up with a plan based on the resources and needs of the accepted proposal.
- **Propose**: EF proposes the plan to vendor, and makes adjustments based on vendor’s feedback
- **Begin**: Vendor accepts and work begins


## Timeline

We expect this project to take around six months, however we also expect this to vary based on things like team size and prior expertise. Proposals should include a projected development timeline which we will actively re-evaluate as the project progresses.


## Deliverables

- Public facing development updates should be published on a 2-week interval.  These can be simple factual updates about what work has been completed and what work is in progress.
- A Specification suitable for broader client adoption.  This will likely be a collection of EIP proposals.
- A mainnet client implementation in a fork of one of the existing mainnet client codebases.
- Presentation of EIP proposals in AllCoreDevs and engagement in AllCoreDevs discussions.


## Fee Structure

### Invoices

The chosen vendor will be expected to submit invoices every 2 months.


### Payment method

The vendor will be given the option to be paid in Fiat money (via bank transfer) or ETH.

If the vendor chooses to be paid in ETH, the value of ETH described under the agreement will be the value in USD at NYSE closing time (4 PM EST) on the day prior to the due date (as described at https://www.coingecko.com).

## Selection Criteria

The selected vendor will have significant expertise in the areas necessary to meet the needs and requirements set forth in this RfP. Particularly:

```
Familiarity with the Ethereum "State" trie
Familiarity with the EVM
```

The scope of this work is large enough that we will be preferring teams over individuals. Individuals are still encouraged to submit a proposal as there may be options available for collaboration.


## Bidding Instructions


Upon reception of this request, interested vendors are expected to confirm receipt and intention to bid on the engagement.

In this confirmation, they should explain what they need from us in order to get started. As well as bring attention to areas in which they feel they do not have significant expertise. We will use this information to try to provide appropriate entrance material for the engagement.

Proposals must be submitted before **TODO**. We expect to take 1 week to deliberate and respond.

Please send initial confirmations, and proposals (in PDF format) to the following address: rfp@ethereum.org

> Feel free to send us any questions you may have: rfp@ethereum.org

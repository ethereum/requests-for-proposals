# State Expiry: Request for Proposals

## Introduction

The Ethereum Foundation would like to announce a Request for Proposals (RfP) for the research and development needed to take the proposed concept for "State Expiry" from its current form into a complete specification and client implementation.

State Expiry is a proposed scheme for introducing economic bounds on the total state size necessary to operate a node on the Ethereum network. The current proposed scheme is currently described in this document: https://hackmd.io/@vbuterin/state_expiry_paths

This proposal is for an open ended engagement with three goals to be implemented in two stages.

1. Stage 1:
    - Additional research into the proposed scheme to validate the approach and gain broader buy in from core devs
2. Stage 2:
    - Implement it in one of the mainnet Ethereum client codebases. (Besu, Geth, Nethermind, OpenEthereum, TurboGeth).
    - A complete specification in the form of an EIP suitable for consideration by core devs and implementations by other client teams.

## Scope

We are looking for an open ended engagement with an individual or team (referred to as "vendor") who can commit their time towards the research and development necessary to bring "State Expiry" to a point where it can be included in the core Ethereum protocol.

The vendor should expect to:

- Leverage communication channels such as the R&D Discord and Research and Magicians forums to engage the core development community
    - Research Forums: https://ethresear.ch/
    - Magicians Forums: https://ethereum-magicians.org/
    - R&D Discord: *Invite available upon request*
- Produce technical write ups and explanations of the proposed scheme


### Stage 1

"State Expiry" is currently only loosely specified in the linked HackMD document. Additional research is necessary to extend what is layed out in the HackMD document into a fully specified set of protocol changes.  In this stage, vendor should focus on gaining a detailed understanding of the problem, producing detailed write ups of what they learn, exploration into potential problems, exploration and understanding of any trade-offs present in the scheme.  This process should include continuous feedback and engagement with the core development community.


### Stage 2

Once research has validated that the scheme appears to be viable, and there is clear buy-in from the core development community, work should shift towards a concrete spec and accompanying implementation in a mainnet Ethereum client.  

- The specification should take the form of one or more EIP documents
- The implementation should be suitable for running a test network

> EIP: Ethereum Improvement Proposals - https://github.com/ethereum/EIPs
    
## Process Summary

The entire process can be summarized as follows:

- **Request**: EF releases RfP (this post)
- **Gather**: Vendors submit proposals
- **Deliberate**: EF decides which proposal to accept, and comes up with a plan based on the resources and needs of the accepted proposal.
- **Propose**: EF proposes the plan to vendor, and makes adjustments based on vendor’s feedback
- **Begin**: Vendor accepts and work begins


## Timeline

We expect this engagement to be open ended with an estimated lower bound of 6 months and upper bound of 18 months.


## Deliverables

- Public facing development updates should be published on a 2-week interval.  These can be simple factual updates about what work has been completed and what work is in progress.
- A Specification suitable for broader client adoption.  This will likely be a collection of EIP proposals.
- A mainnet client implementation in a fork of one of the existing mainnet client codebases.
- Presentation of EIP proposals in AllCoreDevs and engagement in AllCoreDevs discussions.
- Attendence and engagement in public calls such as AllCoreDevs
- Engaging with the EF on experiments, analytics, etc if requested


## Fee Structure

### Invoices

The chosen vendor will be expected to submit invoices every 2 months.


### Payment method

The vendor will be given the option to be paid in Fiat money (via bank transfer) or ETH.

If the vendor chooses to be paid in ETH, the value of ETH described under the agreement will be the value in USD at NYSE closing time (4 PM EST) on the day prior to the due date (as described at https://www.coingecko.com).

## Selection Criteria

The selected vendor will *either* have significant expertise in the areas necessary to meet the needs and requirements set forth in this RfP **or** have sufficient base knowledge and expressed intent to learn. 

Areas of expertise that will be beneficial:

```
Familiarity with the Ethereum "State" trie
Familiarity with the EVM
Familiarity with the concept of imposing economic bounds on the total state size
```

The scope of this work is large enough that we will be preferring teams over individuals. Individuals are still encouraged to submit a proposal as there may be options available for collaboration.

This RfP is intented to be an on-ramp to core protocol development.  We are not interested in "mercenary" work.  Applicants should have an intrinsic interest in continued work on the core Ethereum protocols.


## Bidding Instructions


Upon reception of this request, interested vendors are expected to confirm receipt and intention to bid on the engagement.

In this confirmation, they should explain what they need from us in order to get started. As well as bring attention to areas in which they feel they do not have significant expertise. We will use this information to try to provide appropriate entrance material for the engagement.

Proposals must be submitted before **TODO**. We expect to take 1 week to deliberate and respond.

Please send initial confirmations, and proposals (in PDF format) to the following address: rfp@ethereum.org

> Feel free to send us any questions you may have: rfp@ethereum.org

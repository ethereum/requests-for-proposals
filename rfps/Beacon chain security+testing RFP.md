# Beacon chain security+testing RFP
## Introduction
The Ethereum Foundation (EF) would like to announce a Request for Proposals (RfP) for general security and testing engagements related to the beacon chain and the upcoming merge of Ethereum to the beacon chain.

- [Beacon chain security+testing RFP](https://notes.ethereum.org/@lsankar/security-rfp#Beacon-chain-securitytesting-RFP)
  - [Introduction](https://notes.ethereum.org/@lsankar/security-rfp#Introduction)
  - [Scope](https://notes.ethereum.org/@lsankar/security-rfp#Scope)
  - [Potential areas of focus](https://notes.ethereum.org/@lsankar/security-rfp#Potential-areas-of-focus)
    - [live network analysis](https://notes.ethereum.org/@lsankar/security-rfp#live-network-analysis)
    - [network load testing and simulation](https://notes.ethereum.org/@lsankar/security-rfp#network-load-testing-and-simulation)
    - [client load testing](https://notes.ethereum.org/@lsankar/security-rfp#client-load-testing)
    - [novel fuzzing](https://notes.ethereum.org/@lsankar/security-rfp#novel-fuzzing)
    - [formal verification](https://notes.ethereum.org/@lsankar/security-rfp#formal-verification)
    - [consensus attacks](https://notes.ethereum.org/@lsankar/security-rfp#consensus-attacks)
    - [new consensus test vectors](https://notes.ethereum.org/@lsankar/security-rfp#new-consensus-test-vectors)
    - [merge and sharding r&d](https://notes.ethereum.org/@lsankar/security-rfp#merge-and-sharding-rampd)
- [Process summary](https://notes.ethereum.org/@lsankar/security-rfp#Process-summary)
- [Fee structure](https://notes.ethereum.org/@lsankar/security-rfp#Fee-structure)
  - [Invoices](https://notes.ethereum.org/@lsankar/security-rfp#Invoices)
  - [Payment method](https://notes.ethereum.org/@lsankar/security-rfp#Payment-method)
- [Bidding instructions](https://notes.ethereum.org/@lsankar/security-rfp#Bidding-instructions)

## Scope
The EF will consider any proposals that further the security and robustness of Ethereum’s beacon chain and the upcoming merge (migration from PoW to PoS). In practice, this means any of the specifications or code in:

- [the eth2spec](https://github.com/ethereum/eth2.0-specs)

- any of the following 4 clients:

  * [lighthouse](https://github.com/sigp/lighthouse)

  * [teku](https://github.com/ConsenSys/teku)

  * [prysm](https://github.com/prysmaticlabs/prysm)

  * [nimbus](https://github.com/status-im/nimbus-eth2)

- supporting core libraries (e.g. libp2p libs, crypto libs, etc)

  

  **This is an open call.** The RfP is broad and intended to cover a wide variety of engagements. Proposals should be formed based on your team’s expertise along with the challenges and needs at hand.

  For some ideas around what could constitute a good engagement, see the following section.

## Potential areas of focus
The following are some representative starting points.

This list is neither exhaustive nor is it very detailed. Proposals are expected to be much more fleshed out than anything found here.

### live network analysis
Use tools to gather data and analyzelive beacon chain networks (both testnets and mainnet). There is a lot going on at the network layer and likely much to better understand and improve.
### network load testing and simulation
Use simulation (e.g. using [Protocol Labs’ Testground](https://docs.testground.ai/)) to understand network propagation, finality, and liveness under varied conditions.
### client load testing
Subject beacon chain clients to varied load profiles or under sub-optimal resource consumption to better understand general load, dos vectors, and potential targets for optimization.
### novel fuzzing
[Sigma Prime’s beacon-fuzz](https://github.com/sigp/beacon-fuzz) fuzzes critical state transition targets today. Introduce novel fuzzing methods and targets beyond those already covered by beacon-fuzz.
### formal verification
Apply formal verification techniques to verify the spec, critical tools, components of clients, or cryptographic libraries. Existing work in this domain includes Runtime Verifications [K beacon-chain-spec](https://github.com/runtimeverification/beacon-chain-spec) and [ConsenSys’s dafny spec.](https://github.com/ConsenSys/eth2.0-dafny)
### consensus attacks
Studies of new theoretical attacks on beacon chain consensus.
### new consensus test vectors
Extensions of consensus test vectors to aid client compliance.
### merge and sharding r&d
The two major upgrades coming to the beacon chain are the merge and sharding. Any experiments, research, development, or analysis that helps get us there safely and quickly.
## Process summary
The entire process can be summarized as follows:

1. **Request:** Release of RFP (this post)
2. **Gather:** Vendors submit proposals
3. **Deliberate:** EF decides which proposal(s) to accept, and comes up with a plan based on the resources and needs of the accepted proposal(s).
4. **Propose:** EF proposes the plan to vendor, and makes adjustments based on vendor’s feedback
5. **Begin:** Vendor accepts and work begins

## Fee structure
### Invoices
Based on the timeline of this engagement, the chosen vendor(s) will be expected to submit 2 invoices:
a first invoice of 40% of the total engagement fee at the start of the engagement
a second invoice of 60% of the total engagement fee at the end of the engagement, following the delivery of the summary report and a 5 day review period.
### Payment method
The vendor will be given the option to be paid in Fiat money (via bank transfer) or ETH.
If the vendor chooses to be paid in ETH, the value of ETH described under the agreement will be the value in USD at NYSE closing time (4 PM EST) on the day prior to the due date (as described at [https://www.coingecko.com](https://www.coingecko.com)).
### Bidding instructions
Upon reception of this request, interested vendors are expected to confirm receipt and intention to bid on the engagement.

In this confirmation, they should explain what they need from us in order to get started. As well as bring attention to areas in which they feel they do not have significant expertise. We will use this information to try to provide appropriate entrance material for the engagement.

Proposals must be submitted before April 20th, 2021 at 5pm PST*. We expect to take 1 week to deliberate and respond.

Please send initial confirmations, and proposals (in PDF format) to the following address: rfp@ethereum.org
*Feel free to send us any questions you may have: rfp@ethereum.org*


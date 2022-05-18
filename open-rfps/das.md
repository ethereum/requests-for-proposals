# Data Availability Sampling Networking RFP

The Ethereum Foundation (EF) is seeking proposals for projects looking to contribute to the domain of Data Availability Sampling (DAS) with respect to its implementation in peer to peer networks. This problem domain is under-explored, and we are excited to invite additional teams and individuals to explore this with us.

In particular, the EF is requesting proposals that aim to design, refine, build, analyze, and test both theoretical and practical DAS techniques. This is a critical problem space in Ethereum p2p networking.

The EF has earmarked **$1.5M in funding** for this RFP and is looking to accept not one, but a number of proposals. Proposals can span from formal design/analysis to more practical engineering and testing.

* [Problem statement](#Problem-statement)
* [RFP Details](#RFP-Details)
* [Bidding instructions](#Bidding-instructions)

## Problem statement

### High level

DAS is critical for any blockchain design that provides data availability guarantees beyond the resources of any standard node on the network -- e.g. Layer-1 comes to consensus on 1MB of data per second, but any standard node on the network only has the resources (bandwidth, storage, etc) to validate/download 50kb per second.

In a DAS model, nodes randomly sample data that has been erasure encoded to ensure data is available and (in the event of data being missing or withheld) reconstruct portions of the data.

To read more about the Data Availability problem and DAS please see these resources:
* [A note on data availability and erasure coding](https://github.com/ethereum/research/wiki/A-note-on-data-availability-and-erasure-coding)
* [Fraud and Data Availability Proofs](https://arxiv.org/abs/1809.09044)
* [Recent Ethereum sharding design proposal](https://notes.ethereum.org/@dankrad/new_sharding)
* [DAS Requirements and tools](https://notes.ethereum.org/@djrtwo/das-requirements)

### Requirements

DAS can be divided into a number of problems:
1. Disseminate small amounts of data to all nodes (samples or sets of samples) to support sampling from other nodes, in a way that supports random sampling (see 2)
2. Support queries for random samples in an efficient and safe way
3. Identify and reconstruct missing data (to then disseminate, 1 & 2)

For a deeper discussion of these requirements, please see [here](https://notes.ethereum.org/@djrtwo/das-requirements).

In an exploration of one or more of these requirements, we suggest you parametrize the relevant values and analyze under various considerations (e.g. `DATA_PER_BLOCK`, `NETWORK_NODE_COUNT`, etc)

Note that designs should be analyzed/tested in both the happy case as well as under a diverse adversarial environment -- e.g. where does the design break down, under what type of adversary, what types of attacks are available, etc.; examples of typical attacks on DAS are:
 * Data withholding attacks (attacker overtakes/bribes the validator set to vote for an invalid block)
 * Temporary withholding attack (same attack but attacker later makes the data available)
 * Targeted eclipse attacks, where the attacker makes samples available to a subset of node, but not enough to reconstruct the data
 * DOS attacks, where the attacker breaks data availability sampling in such a way that all or a certain subset of samples are never retrievable
Analyzing these attacks as well as coming up with new ones is part of this RFP.

## RFP Details

As noted above, the EF is looking to accept multiple proposals pertaining to DAS networking that aim to design, refine, build, analyze, and/or test both theoretical and practical DAS techniques.

### Process summary

The entire process can be summarized as follows:

1. **Request:** EF releases RFP (this post)
2. **Gather:** Teams submit proposals
3. **Deliberate:** EF analyzes proposals, discusses dynamically any suggestions in structure, direction, fee schedule, and/or timeline, and comes up with a plan based on the resources and needs of the accepted proposal(s).
4. **Propose:** EF proposes a final structure of the proposal based upon deliberations/discussions.
5. **Begin:** Team accepts and work begins

### Engagement timeline

The EF proposes projects be structured either as 3, 6, or 12 month engagements with milestones/check-ins throughout (more for longer engagements).

Initial proposals will not be accepted for longer than 12 month engagements. Subsequent proposals and grants can be formulated for followup work in the event this engagement goes well and a continuation is warranted.

### Deliverables

The team is expected to define their own deliverables as a part of scoping the project. Deliverables can include but are not limited to -- formal papers, design documents, instructional videos, survey specifications, implementations, creation or extension of library code, experimental results, and blog posts.

## Bidding instructions

Upon reception of this request, interested Teams are expected to confirm receipt and intention to submit a proposal.

In this confirmation, Teams should explain what they need from the EF in order to get started. This is a complex domain -- the EF is happy to help get you up to speed via sharing additional resources and/or answering direct questions.

Proposals must be submitted by July 1, 2022.

Please send initial confirmations, and proposals (in PDF format) to the following  address: rfp@ethereum.org

_Feel free to send us any questions you may have: rfp@ethereum.org_
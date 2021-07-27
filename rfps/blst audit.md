## Introduction

The [Ethereum Foundation](https://ethereum.foundation/) (EF) and [Protocol Labs](https://protocol.ai/) (PL) would like to announce a Request for Proposals (RfP) for a security review of [`blst`](https://github.com/supranational/blst).

[`blst`](https://github.com/supranational/blst) (pronounced ‘blast’) is a BLS12-381 signature library written in C and assembly focused on performance and security.

## Table of Contents



- blst audit
  - [Introduction](https://notes.ethereum.org/@djrtwo/blst-rfp#Introduction)
  - [Table of Contents](https://notes.ethereum.org/@djrtwo/blst-rfp#Table-of-Contents)
  - Preliminaries
    - [BLS signatures](https://notes.ethereum.org/@djrtwo/blst-rfp#BLS-signatures)
    - [Pairings](https://notes.ethereum.org/@djrtwo/blst-rfp#Pairings)
    - [BLS signatures in eth2](https://notes.ethereum.org/@djrtwo/blst-rfp#BLS-signatures-in-eth2)
    - [A note on BLS12-381](https://notes.ethereum.org/@djrtwo/blst-rfp#A-note-on-BLS12-381)
    - [Spec requirements](https://notes.ethereum.org/@djrtwo/blst-rfp#Spec-requirements)
    - [Standardization efforts](https://notes.ethereum.org/@djrtwo/blst-rfp#Standardization-efforts)
    - [Ciphersuites](https://notes.ethereum.org/@djrtwo/blst-rfp#Ciphersuites)
  - [Version of code for audit](https://notes.ethereum.org/@djrtwo/blst-rfp#Version-of-code-for-audit)
  - [Scope of audit](https://notes.ethereum.org/@djrtwo/blst-rfp#Scope-of-audit)
  - [Repository Structure](https://notes.ethereum.org/@djrtwo/blst-rfp#Repository-Structure)
  - [Dependencies](https://notes.ethereum.org/@djrtwo/blst-rfp#Dependencies)
  - [Specific areas of focus](https://notes.ethereum.org/@djrtwo/blst-rfp#Specific-areas-of-focus)
  - [Process summary](https://notes.ethereum.org/@djrtwo/blst-rfp#Process-summary)
  - [Engagement timeline](https://notes.ethereum.org/@djrtwo/blst-rfp#Engagement-timeline)
  - [Deliverables](https://notes.ethereum.org/@djrtwo/blst-rfp#Deliverables)
  - Fee Structure
    - [Invoices](https://notes.ethereum.org/@djrtwo/blst-rfp#Invoices)
    - [Payment method](https://notes.ethereum.org/@djrtwo/blst-rfp#Payment-method)
  - [Selection criteria](https://notes.ethereum.org/@djrtwo/blst-rfp#Selection-criteria)
  - [Bidding instructions](https://notes.ethereum.org/@djrtwo/blst-rfp#Bidding-instructions)



## Preliminaries

### BLS signatures

The [Boneh–Lynn–Shacham](https://en.wikipedia.org/wiki/Boneh–Lynn–Shacham) (BLS) signature scheme allows a user to verify that a signer is authentic.

Signatures are elements of an elliptic curve group, and a [pairing](https://en.wikipedia.org/wiki/Pairing-based_cryptography) is used for verification.

The scheme has a variety of important properties. For our purposes, two distinguishing ones are:

1. **Signature aggregation.** A collection of signatures (signature_1, …, signature_n) can be aggregated into a single signature. Moreover, the aggregate signature can be verified using only 2 pairings, as opposed to 2n pairings, when verifying n signatures separately (verifying a signature requires 2 pairing operations). Furthermore the most expensive part of pairing computation, the final exponentiation, can be done [once per aggregate](https://ethresear.ch/t/fast-verification-of-multiple-bls-signatures/5407).
2. **Threshold signatures.** Threshold signatures allows verifiers to check that a threshold number of nodes have signed something. Specifically, threshold signatures allow for a private key to be spread across multiple nodes. Any subset of these nodes, as long as they are more than some threshold number, can then sign a message, without bringing their private keys together.

### Pairings

A [pairing](https://en.wikipedia.org/wiki/Pairing-based_cryptography) is a bilinear map defined between groups. In the context of BLS signatures, it is a map `e: G1 x G2 --> GT` where `G1`, `G2`, and `GT` are distinct subgroups of the same prime order.

[Pairings](https://medium.com/@VitalikButerin/exploring-elliptic-curve-pairings-c73c1864e627) greatly expand what elliptic curve-based protocols can do, enabling things like threshold signatures, for example.

### BLS signatures in eth2

In eth2, validators are organised into committees to do their work. A vote cast by a validator is called an attestation. And an attestation is comprised of many elements, specifically:

- a vote for the current beacon chain head
- a vote on which beacon block should be justified/finalised
- a vote on the current state of the shard chain
- the signatures of all of the validators who agree with that vote

Attestations are designed to be easily combined such that if two or more validators have attestations with the same votes, they can be combined by adding the signatures fields together in one attestation. This is what we mean by aggregation.

This is the mechanism by which eth2 scales the number of validators. By breaking the validators up into committees, validators need only to care about their fellow committee members and only have to check very few aggregated attestations from each of the other committees.

Eth2 makes use of the aggregation property of BLS signatures to reduce the computational cost. On the specific curve chosen (BLS12-381), signatures are 96 bytes each.

### A note on BLS12-381

[BLS12-381](https://electriccoin.co/blog/new-snark-curve/) is part of a family of curves described by [Barreto, Lynn, and Scott](https://eprint.iacr.org/2002/088.pdf). It’s a curve that’s both secure and optimized for pairing operations.

The 12 is the [embedding degree](https://hackmd.io/@benjaminion/bls12-381#Embedding-degree) of the curve.

The 381 is the number of bits needed to represent a coordinate (in Fq) on the curve: the field modulus, `q`. In other words, the 381 means that the prime in the finite field `Fq` is of 381 bits. The size of this number is guided both by [security requirements](https://hackmd.io/@benjaminion/bls12-381#Security-level) and implementation efficiency.

> Note that the BLS (Barreto-Lynn-Scott) in BLS12-381 is different from the BLS (Boneh–Lynn–Shacham) in BLS signature scheme. The BLS signature scheme works with many curves, BLS and non-BLS.

**Full description**

```
u = -0xd201000000010000

k = 12

q = 0x1a0111ea397fe69a4b1ba7b6434bacd764774b84f38512bf6730d2a0f6b0f6241eabfffeb153ffffb9feffffffffaaab

r = 0x73eda753299d7d483339d80809a1d80553bda402fffe5bfeffffffff00000001

E(Fq) := y^2 = x^3 + 4

Fq2 := Fq[i]/(x^2 + 1)

E'(Fq2) := y^2 = x^3 + 4(i + 1)
```

For a more thorough introduction to the curve, and it’s properties, see [here](https://hackmd.io/@benjaminion/bls12-381).

### Spec requirements

The BLS signature requirements for phase 0 are described in the beacon chain spec [here](https://github.com/ethereum/eth2.0-specs/blob/dev/specs/phase0/beacon-chain.md#bls-signatures).

### Standardization efforts

The relevant IETF standardization efforts are [BLS12-381 curve](https://tools.ietf.org/id/draft-yonezawa-pairing-friendly-curves-02.html), [Hash-To-Curve draft 9](https://tools.ietf.org/html/draft-irtf-cfrg-hash-to-curve-07), and [BLS Signatures draft 2](https://tools.ietf.org/html/draft-irtf-cfrg-bls-signature-02).

### Ciphersuites

A ciphersuite describes the building blocks (a curve, mapping a message to a point on the curve, a signature scheme, magic constants/ID, etc) underpinning a crypto protocol.

For our purposes the relevant ciphersuites are:

- Hash-To-Curve: 

  ```
  BLS12381G2_XMD:SHA-256_SSWU_RO
  ```

  - Curve: BLS12-381
  - Hash_to_curve: targets the G2 curve
  - Hash_to_field_Fp2: produces a pseudo randombytes with expand_xmd
  - Hash function is SHA2-256
  - Mapping_Fp2_to_G2 uses Simplified Shallue-van de Woestijne-Ulas Method
  - RO: hashing uses the “indifferentiable from random oracle” method

- BLS Signatures: `BLS_SIG_BLS12381G2_XMD:SHA-256_SSWU_RO_POP_`

- BLS Proof-of-possession: `BLS_POP_BLS12381G2_XMD:SHA-256_SSWU_RO_POP_`

## Version of code for audit

The github commit of the code for audit will be determined at the start of the audit. The `blst` code is developed in the open at https://github.com/supranational/blst

## Scope of audit

The audit should focus on assessing the security and correctness of the Go and Rust binding implementations, along with the underlying C code found in the `src` directory. Optionally, the assembly found in the `asm` directory can also be considered to be in scope, but proposals will be accepted that do not audit this code.

## Repository Structure

**Root** - Contains various configuration files, documentation, licensing, and a build script

- Bindings

   \- Contains the files that define the blst interface

  - Blst_aux.h - contains experimental functions not yet committed for long-term maintenance

  - Blst.swg - provides definition file for creating blst bindings in Java and Python using SWIG

  - Blst.h - provides C API to blst library

  - blst.hpp - provides prototype C++ API to blst library

  - Go

     \- folder containing Go bindings for blst, including tests and benchmarks?=

    - **Hash_to_curve**: folder containing test for hash_to_curve from IETF specification

  - **Java** - folder containing an example of how to use SWIG Java bindings for blst

  - **Python** - folder containing an example of how to use SWIG Python bindings for blst

  - **Rust** - folder containing Rust bindings for blst, including tests and benchmarks

- Src

   \- folder containing C code for lower level blst functions such as field operations, extension field operations, hash-to-field, and more

  - **Asm** - folder containing perl scripts that are used to generate assembly code for different hardware platforms including x86 with ADX instructions, x86 without ADX instructions, and ARMv8

- Build

   \- this folder containing a set of pre-generated source files for a variety of operating systems. The purpose of this folder is for users who do not want to go through the build process.

  - **Coff** - executable code for use on Unix systems
  - **Elf** - executable code for use on Unix systems
  - **Mach-o** - executable code for use on MacOS systems
  - **Win64** - executable code for use on Windows systems

## Dependencies

The library is intended to be compliant with the following IETF draft specifications:

- [IETF BLS Signature V2](https://tools.ietf.org/html/draft-irtf-cfrg-bls-signature)
- [IETF Hash-to-Curve V9](https://tools.ietf.org/html/draft-irtf-cfrg-hash-to-curve)

## Specific areas of focus

The goal of the audit should be to improve the assurance that the cryptography code is correct and well implemented. Additionally, because this library will be used in a consensus system, it is critical that identical outputs are returned for both the Rust and Go bindings.

## Process summary

The entire process can be summarised as follows:

1. **Request:** Release of RfP (this post)
2. **Gather:** Vendors submit proposals
3. **Deliberate:** EF and PL decide which proposal to accept, and comes up with a plan based on the resources and needs of the accepted proposal.
4. **Propose:** EF and PL propose the plan to vendor, and makes adjustments based on vendor’s feedback
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

Members of the EF, PL, and `blst` contributors will be available at all times to answer questions and comments during the assessment period in order to make life as easy as possible for the vendor.

## Deliverables

Deliverable will take the form of Github issues in the [relevant Github repository](https://github.com/supranational/blst) for every security concern found.

As outlined above, the vendor will provide a report distilling the lessons learnt, and summarising the issues submitted.

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
Expertise in applied cryptography and cryptographic systems
Expertise in low level, optimised code
Experience with the C, Rust, and Go programming languages
Experience with assembly programming
```

The EF, PL, and `blst` maintainers have considerable expertise in these domains and are ready to support the vendor.

## Bidding instructions

Upon reception of this request, interested vendors are expected to confirm receipt and intention to bid on the engagement.

In this confirmation, they should explain what they need from us in order to get started. As well as bring attention to areas in which they feel they do not have significant expertise. We will use this information to try to provide appropriate entrance material for the engagement.

Proposals must be submitted before *September 18th at 5pm PST*. We expect to take 1 week to deliberate and respond.

Please send initial confirmations, and proposals (in PDF format) to the following address: [rfp@ethereum.org](mailto:rfp@ethereum.org)

*Feel free to send us any questions you may have: [rfp@ethereum.org](mailto:rfp@ethereum.org)*
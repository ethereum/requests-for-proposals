# Eth2 deposit CLI security audit: request for proposals




## Introduction




We would like to announce a Request for Proposals (RfP) for a security review of the eth2 deposit CLI (written in python).




This method of approaching auditors is new for us. In the past, we’ve chosen to organise audits by approaching a single auditor directly.




We’re moving in this direction in order to try and get a more diverse pool of auditors on the scene.




This request describes the [eth2 deposit CLI](https://github.com/ethereum/eth2.0-deposit-cli) in detail, the scope of the security assessment, the deliverables expected, and a suggested timeline.




It also provides guidelines on fee structure, selection criteria, and bidding instructions.




### What is eth2?




Eth2 is the next generation of Ethereum. It’s a multi-year plan to improve the scalability, security and programmability of Ethereum, without compromising on decentralization.




In contrast to Ethereum today, eth2 uses proof-of-stake (PoS) to secure its network. And while the current chain will continue to exist as its own independent proof-of-work chain for a little while to come, the transition towards PoS starts with the launch of the [beacon chain (phase 0)](https://notes.ethereum.org/@djrtwo/Bkn3zpwxB) later this year.




### Why are deposits important?




In order to make this transition possible, eth2 requires active participants, known as validators, to deposit ETH as collateral in exchange for receiving rewards for actions that help the network reach consensus.




In a sentence: if deposits can’t happen safely, then there are no validators, and eth2 doesn’t launch.




## Project description




The purpose of the deposit CLI is to provide a secure, simple, offline method for aspiring validators to generate keystores and the [`DepositData`](https://notes.ethereum.org/@djrtwo/Bkn3zpwxB#Deposit) required to become a validator on eth2.




#### Keystores




Keystores are files that contain private keys encrypted with a user’s password. Validator clients use keystores as a method for exchanging keys since they can be safely stored and transferred between computers, provided the password is not stored on the same computer.




The deposit CLI generates a keystore for each validator with the appropriate signing keys.




#### DepositData




`DepositData` is the data supplied by the user to the [deposit contract](https://notes.ethereum.org/@av80r/Eth2-deposit-CLI-audit_RFP) (a necessary step to become a validator).




The deposit CLI generates a JSON file with the necessary `DepositData`.




### Process




#### 0. Clone repository




```

git clone https://github.com/ethereum/eth2.0-deposit-cli.git

```




#### 1. Install dependencies and run CLI




For Linux or MacOS users:




```

./deposit.sh install

./deposit.sh

```




For Windows users:




```

sh deposit.sh install

sh deposit.sh

```




Note that you can also run the CLI (second command) with optional flags:




```

--num_validators=<NUM_VALIDATORS>

--mnemonic_language=english

--folder=<YOUR_FOLDER_PATH>

--chain=<CHAIN_NAME>

```




#### 2. Input preferences




Upon entering the interactive CLI you’re asked to choose the number of validators you wish to run




```

Please choose how many validators you wish to run: 

```




And your preferred language




```

Please choose your mnemonic language (czech, chinese_traditional, chinese_simplified, english, spanish, italian, korean) [english]: 

```




#### 3. Type password to secure keystores & generate mnemonic




You’re then asked to type a password




```

Type the password that secures your validator keystore(s):

Repeat for confirmation: 

```




Correctly confirming the password, generates the Mnemonic.




#### 4. Write down Mnemonic




```

This is your seed phrase. Write it down and store it safely, it is the ONLY way to retrieve your deposit.





weird tool evoke because fish enter review forget panda coffee ceiling stadium car happy strategy proud genius adapt like vocal jewel trial void inspire





Press any key when you have written down your mnemonic.

```




#### 5. Generate keys, keystores, and deposit data




```

Please type your mnemonic (separated by spaces) to confirm you have written it down:

```




Once you’ve proven you’ve written down the mnemonic, you get your keys




```

             #####     #####                                 

                ##     #####     ##                               

    ###         ##   #######     #########################        

    ##  ##      #####               ##                   ##       

    ##     #####                 ##                       ##      

    ##     ##                     ##                      ###     

   ########                        ##                     ####    

   ##        ##   ###         #####                       #####   

   #                          ##                         # #####  

   #                            #                        #  ##### 

   ##                             ##                    ##        

   ##                              ##                   ##        

   ##             ###              ##                   ##        

   ###############                 ##                   ##        

   ###               ##                                 ##        

      #############################                    ##         

                     ##                             ###           

                     #######     #################     ###        

                     ##   ## ##        ##   ##    ###             

                     ##############          #############                                                 

Creating your keys.

Saving your keystore(s).

Creating your deposit(s).

Verifying your keystore(s).

Verifying your deposit(s).



Success!

Your keys can be found at: <YOUR_FOLDER_PATH>

Saving your keystore(s)

```




A Keystore (containing the relevant signing key) is generated for every validator. Note that, to cut down on confusion, validators aren’t given keystores for their withdrawal keys.




```

Creating your deposit(s)

```




A JSON file is created containing the necessary `DepositData`.




### Resources




- [Validated: staking on eth2 #0](https://blog.ethereum.org/2019/11/27/validated-staking-on-eth2-0/): Intro to eth2 and staking

- [Validated: staking on eth2 #4 Keys](https://blog.ethereum.org/2020/05/21/keys/): Key reading ;)

- [EIP 2333](https://eips.ethereum.org/EIPS/eip-2333): BLS Key Generation

- [EIP 2334](https://eips.ethereum.org/EIPS/eip-2334): BLS Deterministic Account Hierarchy

- [EIP 2335](https://eips.ethereum.org/EIPS/eip-2335): BLS Keystore

- [Deposit CLI repository](https://github.com/ethereum/eth2.0-deposit-cli)

- [Deposit Launchpad repository](https://github.com/ethereum/eth2.0-deposit)

- [Deposit Contract repository](https://github.com/ethereum/eth2.0-specs/tree/dev/deposit_contract)

- [Deposit Contract formal verification](https://runtimeverification.com/blog/end-to-end-formal-verification-of-ethereum-2-0-deposit-smart-contract/)

- [eth2 specs](https://github.com/ethereum/eth2.0-specs/blob/v0.10.0/specs/phase0/beacon-chain.md#depositdata): Phase 0, The Beacon Chain

- [Phase 0 for Humans](https://notes.ethereum.org/@djrtwo/Bkn3zpwxB)




## Security assessment scope




The scope of this security engagement includes the review of the following eth2 components:




```

eth2 deposit cli

```




The assessment will focus on identifying vulnerabilities that can lead to the following (non-exhaustive list):




```

- Incorrect generation of the mnemonic

- Incorrect calculation of the withdrawal key

- Incorrect derivation of the signing key

```




Our main concern is the correct calculation of the withdrawal key, since it is not validated anywhere else (the signing key is verified in the deposit launchpad UI). Within this, it will be important to verify that:




```

- The secret key is derived correctly

- Withdrawal credentials == hash(private key)*

- The withdrawal key can be rederived from the mnemonic

```




Other areas of concern include:




```

- Verify that installation instructions are correct on all operating systems

- Verify that Keystore is a valid implementation of EIP 2335

- Verify that deposit_data JSON is a valid representation of DepositData

- Verify the scope for users to input invalid/undesirable flags

- Verify that keys and passwords aren't inadvertantly leaked via memory or log files.**

```




*More formally, withdrawal credentials, as defined [here](https://github.com/ethereum/eth2.0-specs/blob/dev/specs/phase0/deposit-contract.md#withdrawal-credentials), should equal `b'\x00' + hash(public_key)[1:]`.




**For example via shell history. Not via more complicated means such as timing attacks though (e.g. because [py_ecc](https://github.com/ethereum/py_ecc) is not constant time).




## Process summary




The entire process can be summarised as follows:




1. **Request:** EF releases RfP (this post)

2. **Gather:** Vendors submit proposals

3. **Deliberate:** EF decides which proposal to accept, and comes up with a plan based on the resources and needs of the accepted proposal.

4. **Propose:** EF proposes the plan to vendor, and makes adjustments based on vendor’s feedback

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




Members of the EF will be available at all times to answer questions and comments during the assessment period in order to make life as easy as possible for the vendor.




## Deliverables




Deliverable will take the form of Github issues in the [relevant Github repository](https://notes.ethereum.org/@av80r/Eth2-deposit-CLI-audit_RFP) for every security concern found. Our recommended Github issue process can be found [here](https://notes.ethereum.org/@av80r/Eth2-deposit-CLI-audit_RFP).




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

Experience with using the Python programming language

Familiarity with hash functions 

Familiarity with cryptographic signature schemes*

Experience with reviewing software

```




The EF has considerable expertise in these domains and is ready to support the vendor.




*e.g. BLS signatures.




## Bidding instructions




Upon reception of this request, interested vendors are expected to confirm receipt and intention to bid on the engagement.




In this confirmation, they should explain what they need from us in order to get started. As well as bring attention to areas in which they feel they do not have significant expertise. We will use this information to try to provide appropriate entrance material for the engagement.




Proposals must be submitted before *June 12th, 12 PM EST*. We expect to take 1 week to deliberate and respond.




Please send initial confirmations, and proposals (in PDF format) to the following address: [rfp@ethereum.org](mailto:rfp@ethereum.org)




We’re also happy to arrange pre-bid meetings, should you feel there’s a need.




## Summary




While we have conducted audits in the past, this is our first time going down the RfP path. We’re excited to get the ball rolling, and expect to learn a great deal from this experience.




Feel free to send us any questions you may have: [rfp@ethereum.org](mailto:rfp@ethereum.org)
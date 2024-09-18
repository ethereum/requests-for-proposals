# Pectra System Contracts Bytecode Audit RFP

The Ethereum Foundation is soliciting proposals for an audit of the bytecode of three smart contracts related to the Pectra hard fork. These are system contracts to be used by EIPs 2935, 7002, 7251 (linked below). They will be deployed prior to the hard fork or as part of its migration.

## Audit Requirements

The audit should focus **exclusively** on the smart contract bytecode, referenced in the pull requests below. It **should not** encompass all of the EIPs, or client implementations of the EIPs, including their interactions with the contracts. 

The audit should validate whether the contracts' bytecode meet the functionality described in the EIPs. The audit should also highlight any potential security vulnerabilities associated with the contract, both as part of its normal utilization and by malicious users. If and where applicable, the audit should ideally propose fixes or improvements to the contract code.

There is a possibility the EIP authors may make changes to the contract code after the publication of this RFP, although we do not expect their semantics to change significantly. The latest versions of the bytecode will be shared with auditors prior to the beginning of the audit.

### [EIP-2935: Serve historical block hashes from state](https://eips.ethereum.org/EIPS/eip-2935)

The contract contains a ring buffer of historical block hashes and two code paths, `get` and `set`, depending on the caller. Expected calldata formats and behavior for each are specified in the EIP.

### [EIP-7002: Execution layer triggerable withdrawals](https://eips.ethereum.org/EIPS/eip-7002)

The contract contains a queue of staking withdrawal requests and three code paths depending on the caller and input: `add_withdrawal_request`, `get_excess_withdrawal_requests`, and `read_withdrawal_requests`. Excess withdrawal requests beyond what the consensus layer can process are queued and a fee is calculated to prevent spam requests.

In addition to the semantics in the EIP, the audit should evaluate the contract behavior prior to the first system call -- noting the initial withdrawal request fee. The first system call will occur in the first block following the hard fork, but the contract can be called before then.

A [geas](https://github.com/fjl/geas) implementation of the contract can be found in [this repository](https://github.com/lightclient/sys-asm).

### [EIP-7251: Increase the MAX_EFFECTIVE_BALANCE](https://eips.ethereum.org/EIPS/eip-7251)

The contract contains a queue of requests to consolidate validators in response to a consensus layer parameter change. It contains three code paths depending on the caller and input: `add_consolidation_request`, `get_excess_consolidation_requests`, and `process_consolidation_requests`. A fee is charged for consolidation requests based on excess requests to be processed, similar to 7002.

In addition to the semantics in the EIP, the audit should evaluate the contract behavior prior to the first system call -- noting the consolidation request fee calculated using `EXCESS_INHIBITOR`.

A [geas](https://github.com/fjl/geas) implementation of the contract can be found in [this repository](https://github.com/lightclient/sys-asm).

## Proposal Submission

To submit a bid for the audit, please email your proposal to rfp@ethereum.org with the subject line &#34;Pectra System Contracts Bytecode Audit&#34; by October 11, 2024. 

Proposals should include a summary of work to be performed, a timeline for completion of the audit, and a price for the engagement. Proposals will be judged on technical expertise, possible start dates, and cost, at the discretion of the Ethereum Foundation.

Accepted proposals will be confirmed by October 22, 2024 at the latest.

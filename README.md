

# STX-Civitas - DAO Governance Smart Contract

A decentralized governance system built in Clarity for Stacks blockchain. This contract enables token-weighted decision-making through community proposals and voting mechanisms, ensuring on-chain transparency, adaptability, and decentralized control.

---

## 📜 Overview

This smart contract provides a framework for a **Decentralized Autonomous Organization (DAO)**, where governance is driven by the token holders. Key features include:

* ✅ Proposal creation by token holders
* 🗳️ Voting weighted by token ownership
* 🧠 Automatic status calculation and proposal execution
* ⚙️ Configurable governance parameters
* 🔐 Ownership-controlled administrative functions

---

## 🧩 Features

### 🔧 Proposal Lifecycle

1. **Create Proposal**: Any token holder with enough balance (above the proposal fee) can submit a proposal.
2. **Vote**: Community members can vote **for**, **against**, or **abstain**.
3. **Status Update**: Once the proposal ends, status is updated based on quorum and majority vote.
4. **Execute**: Passed proposals can be executed on-chain.

### 🗳️ Voting

* Vote types: `for`, `against`, `abstain`
* Token-weighted: each voter's vote is weighted by their token balance.
* No double voting: each address can vote only once per proposal.

### 🔐 Admin Controls

* Mint tokens (for simulation/testing)
* Update:

  * Proposal fee
  * Minimum proposal duration
  * Default quorum threshold

---

## 📂 Contract Structure

### Constants & Enums

* **Vote types**: `vote-type-for`, `vote-type-against`, `vote-type-abstain`
* **Proposal status**: `status-active`, `status-passed`, `status-rejected`, `status-executed`

### Data Maps

* `proposals`: Stores proposals with metadata.
* `votes`: Tracks each voter’s input on proposals.
* `token-balances`: Token ownership mapping.

### Variables

* `total-token-supply`: Initial 10,000,000 tokens.
* `min-proposal-duration`: Defaults to 144 blocks (\~1 day).
* `default-quorum-threshold`: 2,000 tokens (20% of supply).
* `proposal-fee`: 100 tokens.
* `next-proposal-id`: Tracks next available proposal ID.

---

## 🧪 Simulation & Testing Functions

* **`mint-tokens`**: Admin-only, mints tokens to users for testing.
* **`get-proposal-results`**: View voting outcomes.
* **`get-proposal` / `get-vote` / `is-proposal-active`**: Retrieve internal state data.

---

## 🚀 How It Works

### 1. Proposal Creation

```clojure
(create-proposal "Title" "Description" "Link" duration quorum-threshold)
```

* Requires a minimum token balance (`proposal-fee`)
* Must meet minimum duration and quorum settings

### 2. Voting

```clojure
(vote proposal-id vote-type)
```

* Checks for active proposals and token balance
* Records vote with timestamp and vote weight

### 3. Proposal Execution

```clojure
(execute-proposal proposal-id)
```

* Can only be called if the proposal passed and not yet executed

---

## ⚠️ Errors

| Code   | Meaning                   |
| ------ | ------------------------- |
| `u100` | Unauthorized access       |
| `u101` | Proposal already exists   |
| `u102` | Proposal not found        |
| `u103` | Proposal expired          |
| `u104` | Proposal not expired      |
| `u105` | Already voted             |
| `u106` | Insufficient tokens       |
| `u107` | Not proposal creator      |
| `u108` | Proposal already executed |
| `u109` | Invalid proposal duration |
| `u110` | Invalid quorum            |
| `u111` | Not contract owner        |
| `u112` | Proposal not active       |
| `u113` | Proposal not passed       |
| `u114` | Invalid vote type         |

---

## 👨‍💻 Admin Functions

```clojure
(update-proposal-fee new-fee)
(update-min-proposal-duration new-duration)
(update-default-quorum-threshold new-threshold)
```

Only callable by the contract owner (`tx-sender` at contract deploy time).

---

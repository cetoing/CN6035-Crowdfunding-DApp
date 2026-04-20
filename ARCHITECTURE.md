# Architecture Overview

## High-Level Flow

```text
User
  |
  v
Next.js / React frontend
  |
  v
MetaMask wallet
  |
  v
Hardhat JSON-RPC network
  |
  v
Crowdfunding.sol factory contract
  |
  v
Project.sol campaign contracts
```

## Main Components

| Component | Responsibility |
| --- | --- |
| MetaMask | Provides wallet connection and signs user transactions. |
| Next.js frontend | Provides the user interface for campaign creation, contribution, and withdrawal workflows. |
| Redux store | Maintains connected account, Web3 connection, contract instance, projects, and contribution state. |
| Web3.js | Creates contract instances and sends blockchain calls/transactions. |
| Crowdfunding.sol | Creates campaigns and stores all project contract addresses. |
| Project.sol | Enforces campaign rules, contribution validation, state changes, withdrawal requests, and voting. |
| Hardhat | Provides local blockchain, accounts, compilation, deployment, and automated tests. |

## Main User Workflows

### Create Campaign

1. User connects MetaMask.
2. Frontend reads the connected account.
3. User submits campaign title, description, deadline, target contribution, and minimum contribution.
4. Frontend sends a transaction to `Crowdfunding.createProject`.
5. Smart contract deploys a new `Project` contract.
6. `ProjectStarted` event is emitted and displayed in the frontend.

### Contribute to Campaign

1. User enters an ETH contribution amount.
2. Frontend validates the amount against the displayed minimum contribution.
3. MetaMask signs the contribution transaction.
4. `Crowdfunding.contribute` forwards ETH to the relevant `Project` contract.
5. `Project.contribute` checks deadline, state, and minimum contribution.
6. Raised amount and contributor records are updated on-chain.

### Withdrawal Request and Voting

1. Campaign reaches the target and becomes `Successful`.
2. Campaign creator creates a withdrawal request.
3. Contributors vote on the withdrawal request.
4. Creator withdraws the requested amount after the voting threshold is met.
5. The request is marked completed to prevent repeated withdrawal.

## Distributed Systems Relevance

This DApp demonstrates distributed system principles because the core campaign state is stored and enforced by smart contracts rather than a centralized application server. Users interact with the same shared ledger state through signed wallet transactions. The frontend acts as an interface, but the important rules around funding, voting, and withdrawal are enforced on-chain.

## Critical Design Notes

- The project is appropriate for local demonstration because Hardhat provides deterministic accounts and a repeatable blockchain environment.
- The factory pattern separates campaign registry logic from individual campaign logic.
- The withdrawal voting mechanism demonstrates decentralized control over fund release.
- The hardcoded contract address is acceptable for a local coursework demo but should be replaced by environment-specific configuration in a production system.
- The project would need dependency upgrades and security review before any production deployment.


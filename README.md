# CN6035 Hybrid Crowdfunding DApp

This repository contains the CN6035 Mobile and Distributed Systems coursework implementation based on the open-source project:

https://github.com/spandan114/Crowdfunding-DAPP

The project is a crowdfunding decentralized application (DApp). Users can create fundraising campaigns, contribute ETH through MetaMask, and approve withdrawal requests through contributor voting. The application combines a web front end with Solidity smart contracts deployed to a local Hardhat blockchain.

## Coursework Relevance

The project maps to the CN6035 assessment criteria as follows:

| Assessment area | Evidence in this repository |
| --- | --- |
| Back-end implementation | Solidity contracts in `contracts/Crowdfunding.sol` and `contracts/Project.sol` implement campaign creation, contribution handling, project state, withdrawal requests, and contributor voting. |
| Blockchain interaction | Hardhat is used for compilation, testing, local blockchain execution, and contract deployment. The frontend connects to the deployed contract through Web3.js and MetaMask. |
| Front-end implementation | The `client` folder contains a Next.js/React interface with dashboard, campaign creation, contribution, project details, and withdrawal request pages. |
| Code quality and version control | The project includes contract tests, ESLint checks, a verification document, and coursework-specific commits showing the changes made for the assessment. |

## Main Technologies

- Solidity
- Hardhat
- ethers.js
- Web3.js
- MetaMask
- Next.js
- React
- Redux
- Tailwind CSS
- Chai / ethereum-waffle

## Project Structure

```text
.
|-- client/                  # Next.js frontend
|-- contracts/               # Solidity smart contracts
|-- scripts/                 # Hardhat deployment scripts
|-- test/                    # Hardhat contract tests
|-- COURSEWORK_VERIFICATION.md
|-- hardhat.config.js
|-- package.json
```

## Smart Contract Summary

`Crowdfunding.sol` works as the project factory and registry. It creates new `Project` contracts, stores the list of created projects, and forwards user contributions.

`Project.sol` stores the core campaign logic:

- campaign creator
- minimum contribution
- campaign deadline
- target contribution
- raised amount
- contributor count
- project state: `Fundraising`, `Expired`, or `Successful`
- withdrawal request data
- contributor votes

The withdrawal process requires contributor approval before funds are released, which demonstrates blockchain-based rule enforcement and shared distributed state.

## Front-End Summary

The frontend is implemented in the `client` directory. Important areas include:

- `pages/dashboard.js`: displays projects and contribution actions
- `pages/project-details/[id].js`: displays project details and withdrawal requests
- `pages/my-contributions.js`: displays the connected user's contributions
- `components/FundRiserForm.js`: creates new fundraising campaigns
- `components/FundRiserCard.js`: displays campaign state and contribution controls
- `redux/interactions.js`: handles Web3.js contract interaction

## Coursework Changes Made

The original repository was adapted and verified for the 2026 coursework environment:

- Fixed stale 2022/2023 test deadlines by replacing them with future timestamps, allowing the test suite to run correctly in 2026.
- Removed a synchronous external Font Awesome script and replaced the mobile menu icon with a local character.
- Added `passHref` to Next.js `Link` components where required.
- Escaped an apostrophe in JSX to satisfy React linting.
- Added `*.log` to `.gitignore`.
- Added `COURSEWORK_VERIFICATION.md` with verification results and local demo notes.

## Installation

Install root dependencies:

```powershell
npm.cmd install
```

Install frontend dependencies:

```powershell
cd client
npm.cmd install
```

## Compile and Test

From the repository root:

```powershell
npx.cmd hardhat compile
npx.cmd hardhat test
```

Verified result:

```text
15 passing
```

Hardhat may show a Node.js compatibility warning on Node.js 22 because this is an older Hardhat project. The contracts still compile and the tests pass locally.

## Run Locally

Start the local Hardhat blockchain:

```powershell
npx.cmd hardhat node
```

Deploy the crowdfunding contract:

```powershell
npx.cmd hardhat run scripts/deploy.js --network localhost
```

The local deployment address used by the frontend is:

```text
0x5FbDB2315678afecb367f032d93F642f64180aa3
```

Start the frontend:

```powershell
cd client
$env:NODE_OPTIONS="--openssl-legacy-provider"
npm.cmd run dev
```

Open:

```text
http://localhost:3000
```

## MetaMask Local Network

Use these settings:

- Network name: Hardhat Localhost
- RPC URL: `http://127.0.0.1:8545`
- Chain ID: `31337`
- Currency symbol: `ETH`

Import one of the Hardhat test accounts printed in the terminal. These accounts are public development accounts and must never be used on mainnet.

## Verification Results

The following checks were completed locally:

| Check | Result |
| --- | --- |
| `npx.cmd hardhat compile` | Passed |
| `npx.cmd hardhat test` | Passed with `15 passing` |
| `npx.cmd eslint .` in `client` | Passed with warnings only |
| `npm.cmd run build` in `client` | Passed with `NODE_OPTIONS=--openssl-legacy-provider` |
| Local frontend runtime | HTTP `200` at `http://127.0.0.1:3000` |

## Known Limitations

- The project uses older dependencies and `npm audit` reports vulnerabilities.
- The Hardhat version is old and warns when used with Node.js 22.
- The frontend requires the OpenSSL legacy provider flag on modern Node.js.
- The local contract address is hardcoded in `client/redux/interactions.js`.
- ESLint reports remaining React hook dependency warnings.

These limitations are discussed in the coursework technical report as part of the code quality and critical evaluation sections.


# CN6035 Coursework Verification

## Original Repository

https://github.com/spandan114/Crowdfunding-DAPP

## Project Summary

This project is a crowdfunding decentralized application using:

- Solidity smart contracts
- Hardhat local blockchain and testing
- Next.js and React frontend
- Redux for application state
- Web3.js and MetaMask for blockchain interaction

## Coursework Changes

The following small changes were made to verify and improve the project for the coursework demonstration:

- Updated stale 2022/2023 test deadlines to use future timestamps, allowing the contract tests to run correctly in 2026.
- Added a guard around `window.ethereum` listener registration so the app can open safely before MetaMask is injected.
- Removed a synchronous external Font Awesome script from `_document.js` and replaced the mobile menu icon with a local text character.
- Added `passHref` to several Next.js `Link` components to resolve lint issues.
- Escaped an apostrophe in `my-contributions.js` to satisfy React linting.
- Added `*.log` to `.gitignore` so local runtime logs are not committed.

## Verification Results

These checks were completed locally:

- `npx.cmd hardhat compile`: passed
- `npx.cmd hardhat test`: passed with `15 passing`
- `npx.cmd eslint .` in `client`: passed with warnings only
- `npm.cmd run build` in `client`: passed using `NODE_OPTIONS=--openssl-legacy-provider`
- Local frontend runtime: returned HTTP `200` at `http://127.0.0.1:3000`
- UI demo flow: created a local campaign and contributed ETH through the frontend

## Local Demo Notes

Run the Hardhat node:

```powershell
npx.cmd hardhat node
```

Deploy the contract:

```powershell
npx.cmd hardhat run scripts/deploy.js --network localhost
```

Run the frontend:

```powershell
cd client
$env:NODE_OPTIONS="--openssl-legacy-provider"
npm.cmd run dev
```

Open:

```text
http://localhost:3000
```

Use MetaMask with:

- RPC URL: `http://127.0.0.1:8545`
- Chain ID: `31337`

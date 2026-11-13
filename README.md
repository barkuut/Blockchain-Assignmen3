# MG3012 Assignment 3: Smart Contracts with Truffle and Ganache

| | |
|---|---|
| **Student** | Muhammad Bin Barkaat |
| **Course** | MG3012 Blockchain Technology for Business (BSFT, Fall 2026) |
| **Instructor** | Dr. Usama Arshad |
| **GitHub** | https://github.com/barkuut/Blockchain-Assignmen3 |

## Overview

A dApp deployed to a local Ganache blockchain using Truffle. It extends Assignment 2 by moving the MessageBoard contract from Remix and the Sepolia testnet to a Truffle project running on a local network.

## Contracts

| Contract | File | Description |
|---|---|---|
| MessageBoard | `contracts/SmartContract.sol` | Contract from Assignment 2. Anyone can call `setMessage`. Only the owner can call `resetMessage`. |
| Voting (bonus) | `contracts/Voting.sol` | Owner adds candidates. Each address can vote once. |

The frontend uses HTML, CSS and JavaScript with ethers.js v6. It works with MetaMask or directly with Ganache.

## Project Structure

```
contracts/       SmartContract.sol, Voting.sol
migrations/      1_deploy_contract.js, 2_deploy_voting.js
test/            messageboard.test.js
frontend/        index.html, script.js, style.css
screenshots/     compile, migrate, test and UI screenshots
truffle-config.js
package.json
bs-config.json
README.md
```

## Setup

1. Install Node.js (v16 or later), then run:

   ```bash
   npm install -g truffle
   npm install
   ```

   The second command installs lite-server, which serves the frontend.

2. Install Ganache using one of these options:
   - GUI: download from https://archive.trufflesuite.com/ganache
   - CLI: run `npx ganache --port 7545`

3. Start Ganache on `127.0.0.1:7545`. If you use port 8545, update `truffle-config.js` and `frontend/script.js`.

## Commands

```bash
truffle version
truffle compile
truffle migrate --reset
truffle test
npm run dev
```

| Command | Purpose |
|---|---|
| `truffle version` | Check the installed versions |
| `truffle compile` | Compile the contracts |
| `truffle migrate --reset` | Deploy both contracts to Ganache |
| `truffle test` | Run the tests in `test/` |
| `npm run dev` | Serve the frontend at http://localhost:3000 |

The project skeleton was created with `truffle init`, and the Assignment 2 contract was copied into `contracts/`.

## Testing the dApp

1. Start Ganache, then run `truffle migrate --reset` and `npm run dev`.
2. Open http://localhost:3000 in your browser.
3. Click **Connect**. Without MetaMask, the page uses the first Ganache account automatically.
4. Read the current message, update it, reset it using the owner account (Ganache account 0), and vote for a candidate.
5. Each action is a transaction that appears in the Ganache log.

### Optional: MetaMask

1. Add a custom network with RPC URL `http://127.0.0.1:7545`.
2. Set the chain ID to `1337` (or `5777` for older Ganache GUI versions).
3. Import a private key from Ganache.
4. Reload the page and approve the connection.

## Screenshots

All screenshots are in the `screenshots/` folder:

| File | Shows |
|---|---|
| `01_truffle_version.png` | Installed Truffle, Ganache, Solidity and Node versions |
| `02_ganache_running.png` | Ganache running on port 7545 |
| `03_truffle_compile.png` | Successful compilation |
| `04_truffle_migrate.png` | Deployment of both contracts |
| `05_truffle_test.png` | Five tests passing |
| `06_dapp_connected.png` | dApp connected to Ganache |
| `07_dapp_update.png` | Message updated with a confirmed transaction |
| `08_dapp_vote.png` | Vote recorded in the Voting contract |
| `09_ganache_transactions.png` | Transactions in the Ganache log |

## Troubleshooting

| Problem | Fix |
|---|---|
| Contract has no deployments | Run `truffle migrate --reset` first. The frontend reads `build/contracts/*.json`. |
| Invalid opcode or PUSH0 error | The config pins Solidity 0.8.20 with the `paris` EVM version to avoid this. |
| Connection refused | Check that the Ganache port matches `truffle-config.js` and `script.js`. |
| `npm` blocked in PowerShell | Run `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned` |

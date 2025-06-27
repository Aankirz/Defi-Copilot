# rulesv0.md  
This file defines the coding standards, project layout, branch strategy, and checkpoints for **v0** of the DeFi CoPilot hackathon project. By following these rules you’ll end v0 with a clean, demo-ready single‐chain vault integrated with a Chainlink price feed and a minimal UI.

---

## Table of Contents  
1. Overview  
2. Branching & Versioning  
3. Repository Structure  
4. Environment Setup  
5. Coding Conventions  
   • Solidity  
   • JavaScript / React  
6. Testing Requirements  
7. Deployment & Scripts  
8. v0 Milestones & Demo Checklist  

---

## 1. Overview  
v0 Goal:  
- Implement a single‐chain Ethereum vault contract (`CoPilotVault.sol`) that accepts ETH deposits and mints shares.  
- Build a strategy manager contract (`StrategyManager.sol`) that reads an on‐chain Chainlink ETH/USD price feed.  
- Create a minimal Next.js frontend allowing wallet connect, deposit/withdraw, and live price + share balance display.  
- Demonstrate end‐to‐end flow on a testnet (Goerli/Sepolia).

---

## 2. Branching & Versioning  
- Branch from `main` → create `v0-init`  
- Work exclusively in `v0-init` until all v0 checkpoints are complete.  
- Commit messages follow Conventional Commits:  
  • feat(vault): implement deposit()  
  • fix(ui): correct price display decimals  
- Tag release after v0 demo: `v0.0.1`

---

## 3. Repository Structure  
At project root:
- `/contracts` → Solidity sources  
- `/scripts`   → Deployment scripts  
- `/test`      → Unit tests  
- `/frontend`  → Next.js UI  
- `hardhat.config.js`  
- `package.json`  
- `rulesv0.md`  

---

## 4. Environment Setup  
1. Create `.env` in project root (gitignored):  
   ```
   PRIVATE_KEY=0xYOUR_TESTNET_KEY
   ALCHEMY_API_KEY=YOUR_ALCHEMY_KEY
   ```
2. Install dependencies:  
   ```
   npm install
   npm install --save-dev hardhat @nomiclabs/hardhat-ethers
   npm install @chainlink/contracts ethers dotenv
   ```
3. Configure `hardhat.config.js` to read `.env` and connect to Goerli/Sepolia.

---

## 5. Coding Conventions

### Solidity  
- SPDX license + pragma solidity on top.  
- Use `uint256` for all integer arithmetic.  
- Explicit function visibility.  
- NatSpec comments for public/external functions.  
- Revert with clear `require` messages.  
- Contract layout:  
  1. Imports & Pragma  
  2. State variables  
  3. Constructor  
  4. External/Public functions  
  5. Internal/Private helpers  
- Keep each contract under 200 lines if possible.

### JavaScript / React (Frontend)  
- Use ES6+ syntax and async/await.  
- Single React component in `pages/index.js` is acceptable for v0.  
- Keep UI minimal: two buttons, two data fields.  
- No secret keys in the frontend.  
- Use `ethers.js` for contract interactions.  
- Store addresses in `frontend/.env.local`.

---

## 6. Testing Requirements  
- Write unit tests in `/test` with Hardhat + Mocha + Chai.  
- Tests must cover:  
  • deposit() mints correct shares  
  • withdraw() burns shares & returns ETH  
  • `getLatestPrice()` returns a valid int (use mocks)  
- Aim for ≥ 75% coverage on v0 contracts.  
- Run tests locally:  
  ```
  npx hardhat test
  ```

---

## 7. Deployment & Scripts  
- `/scripts/deploy_v0.js`:  
  • Deploy `CoPilotVault.sol`  
  • Deploy `StrategyManager.sol` with Goerli ETH/USD feed address  
  • Print deployed addresses  
- Run:  
  ```
  npx hardhat run --network goerli scripts/deploy_v0.js
  ```
- After deploy, record addresses in `frontend/.env.local` as:  
  ```
  NEXT_PUBLIC_VAULT_ADDRESS=0x...
  NEXT_PUBLIC_MANAGER_ADDRESS=0x...
  ```

---

## 8. v0 Milestones & Demo Checklist  
By the end of v0, ensure you can demo all of the following:

[ ] **Contract Deployment**  
    • CoPilotVault deployed on testnet  
    • StrategyManager deployed with correct feed address  

[ ] **Core Contract Functionality**  
    • `deposit()` mints 1 share per wei deposited  
    • `withdraw()` burns shares & transfers correct ETH  
    • `getLatestPrice()` returns Chainlink price (8 decimals)  

[ ] **Minimal Frontend**  
    • Connect wallet via MetaMask  
    • Show live ETH/USD price from StrategyManager  
    • Show user’s share balance in the vault  
    • Buttons: Deposit 0.01 ETH, Withdraw 0.01 ETH  
    • “Refresh” button to manually update data  

[ ] **Testing**  
    • Unit tests for vault + manager pass  
    • Coverage report indicates ≥ 75% code coverage  

[ ] **Demo**  
    • Deploy scripts run without errors  
    • Frontend loads and interacts with contracts  
    • Able to deposit & withdraw on testnet while viewing price and share data  

Once all items are green, merge `v0-init` into `main` (or tag `v0.0.1`) and proceed to v1.  

---  
_End of rulesv0.md_
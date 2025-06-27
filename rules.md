# DeFi CoPilot – Development Rules & Roadmap

This `rules.md` captures coding standards, branching & release strategy, project structure, and step-by-step milestones from **v0 → v1 → vFinal**. Follow these rules to deliver clean, battle-tested code and demo-ready milestones at each stage.

---

## Table of Contents  
1. Overview  
2. Repository Structure  
3. Branching & Versioning  
4. Commit & PR Guidelines  
5. Environment & Secrets  
6. Coding Conventions  
   • Solidity  
   • JavaScript / TypeScript  
7. Testing Requirements  
8. Deployment & Scripts  
9. v0, v1, vFinal Milestones  
10. Demo & Documentation Checklist  

---

## 1. Overview  
Deliver a secure, maintainable, and well-documented AI-driven cross-chain DeFi CoPilot.  
• v0: Single-chain vault + Chainlink price feed + simple UI  
• v1: On-chain automation (Chainlink Automation) + static cross-chain demo (CCIP)  
• vFinal: Dynamic AI orchestration (ElizaOS + AWS Bedrock) + full cross-chain rebalances

---

## 2. Repository Structure  
Root folders and key files:
- `/contracts` → Solidity sources  
- `/scripts` → Hardhat deploy & utilities  
- `/test` → Hardhat unit tests  
- `/frontend` → Next.js UI  
- `/orchestrator` → Node.js ElizaOS + Bedrock agents  
- `hardhat.config.js` → network & plugin config  
- `package.json` → dependencies & scripts  
- `README.md` → high-level project overview  
- `rules.md` → this file

---

## 3. Branching & Versioning  
- `main` → polished vFinal code  
- `v0-init` → baseline vault + feed  
- `v1-automation-ccip` → automation + CCIP  
- Feature branches off of version branches: e.g. `v0-add-tests`, `v1-ui-enhancements`

Tag releases:  
- `v0.0.1` → MVP deployed  
- `v1.0.0` → automation + CCIP demo  
- `vFinal.1.0.0` → full AI orchestration

---

## 4. Commit & PR Guidelines  
- Use Conventional Commits:  
  • feat(scope): description  
  • fix(scope): description  
  • chore: description  
- PR Titles: `[v0] feat(vault): implement deposit()`  
- Include linked issue or milestone (use GitHub issues if desired)  
- Require at least one reviewer and passing CI checks before merge  

---

## 5. Environment & Secrets  
- Store secrets in `.env` or `.env.local` (do NOT commit).  
- Example `.env`:  
  ```
  PRIVATE_KEY=0x…
  ALCHEMY_API_KEY=…
  AWS_ACCESS_KEY_ID=…
  AWS_SECRET_ACCESS_KEY=…
  BEDROCK_MODEL_ID=…
  ```
- Add `.env*` to `.gitignore`.

---

## 6. Coding Conventions  

### 6.1 Solidity  
- SPDX license + pragma at top of every file.  
- Use NatSpec for public functions and events.  
- Contract layout:  
  1. Imports & Pragma  
  2. Errors & Events  
  3. Storage (state variables)  
  4. Constructor  
  5. External/public functions  
  6. Internal/private functions  
  7. Modifiers & helpers  
- Explicit visibility (`public`, `external`, `internal`, `private`).  
- Prefer `uint256` over other integer sizes.  
- Use `require()` with custom error messages (or custom errors in 0.8.4+).  
- Favor immutable for constants set in constructor.  
- Write unit tests targeting 100% of branches.

### 6.2 JavaScript / TypeScript  
- Follow Airbnb or Standard style.  
- Use `eslint` + `prettier` config at root.  
- Async/await for all asynchronous ops.  
- Never log secrets.  
- Modularize code into small functions.  
- Use TypeScript in `/frontend` and `/orchestrator` if possible; otherwise add JSDoc.

---

## 7. Testing Requirements  
- Use Hardhat + Mocha + Chai.  
- Coverage ≥ 80%.  
- Tests reside in `/test`, matching contract names.  
- Mock Chainlink feeds locally using `deployMocks.js`.  
- CI runs `npx hardhat test` and coverage check.

---

## 8. Deployment & Scripts  
- All deploy scripts in `/scripts`, named by version:  
  • `deploy_v0.js`  
  • `deploy_v1.js`  
- Use Hardhat tasks for common utilities (e.g. `npx hardhat accounts`).  
- Each script logs: contract addresses, network, deployer.  
- After deploy, generate `deployed.json` with addresses for UI & orchestrator.

---

## 9. Milestones & Checkpoints  

### v0 – Single-Chain MVP  
Branch: `v0-init`  
1. Implement `CoPilotVault.sol`: deposit/withdraw, mint/burn shares.  
2. Implement `StrategyManager.sol`: read Chainlink ETH/USD feed.  
3. Deploy on Goerli via `scripts/deploy_v0.js`.  
4. Build minimal Next.js UI in `/frontend`:  
   - Connect wallet, deposit/withdraw, display price & share balance.  
5. Write unit tests for vault & manager.  

✅ **Checkpoint:** Demo deposit/withdraw + live price update.

### v1 – Automation + Static Cross-Chain  
Branch: `v1-automation-ccip`  
1. Add `Rebalancer.sol` with Chainlink Automation (register upkeep).  
2. Create `TargetAllocation.sol` to store static weights.  
3. Add `CCIPAdapter.sol` for bridging assets.  
4. Extend UI: “Set Targets”, “Next Rebalance”, “Bridge Assets” buttons.  
5. Deploy on two testnets; register automation.  
6. Demo cross-chain manual bridge + auto-rebalance on chain A.  

✅ **Checkpoint:** Show scheduled rebalance + CCIP bridge in UI.

### vFinal – AI Orchestration & Polishing  
Branch: `main`  
1. Build `/orchestrator` with ElizaOS agents:  
   - YieldScout, RiskGuardian, MasterAgent.  
2. Integrate AWS Bedrock: fine-tuned model call in YieldScout.  
3. Use Chainlink Functions or signed TX to push dynamic targets to `TargetAllocation.sol`.  
4. Update `Rebalancer.sol` to read dynamic targets.  
5. Polish UI with activity logs, graphs, AI rationale.  
6. Comprehensive E2E tests on local for dynamic rebalance.  
7. Record 3–5 min demo; update `README.md`.  

✅ **Checkpoint:** Full AI-driven cross-chain rebalance demo + code & video submission.

---

## 10. Demo & Documentation Checklist  
- [ ] Public GitHub repo; clear README with architecture diagram.  
- [ ] Code comments & NatSpec for all contracts.  
- [ ] Unit tests & coverage report.  
- [ ] Deployed addresses JSON for UI & orchestrator.  
- [ ] Demo video (3–5 min) explaining:  
  1. Problem & solution overview  
  2. vFinal architecture (contracts, Chainlink services, AI agents)  
  3. Live user flow: deposit → AI rebalance → cross-chain asset moves → withdrawal  
- [ ] Application submission form with video link, GitHub repo, README.

---

Follow this plan and rules rigorously to deliver a robust, production-quality DeFi CoPilot that hits every hackathon track. Good luck! 🚀
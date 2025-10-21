# Base-contract-deploy
Contract deploy on Base Mainnet

# 🧠 Safe Solidity Contracts Collection

This repository contains **five secure and minimal Solidity contracts** designed for safe deployment, learning, and ecosystem building (e.g., Base, Ethereum, or Layer2 environments).

All contracts use **Solidity ^0.8.0**, which includes built-in overflow/underflow protection.

---

## 🔢 Contract List

1️⃣ **BasicMath.sol** — Safe arithmetic operations with manual overflow/underflow checks  
2️⃣ **SafeMathPlus.sol** — Enhanced math contract with revert protection and events  
3️⃣ **SafeStore.sol** — Secure owner-only key/value storage  
4️⃣ **SafeVault.sol** — Simple ETH deposit & withdrawal vault with reentrancy safety  
5️⃣ **UniqueTxLogger.sol** — Generates unique transaction IDs for on-chain tracking  

---

## ⚙️ Deployment Guide (via Remix)

### 🪄 Step-by-Step

1️⃣ **Open Remix IDE**  
🔗 [https://remix.ethereum.org](https://remix.ethereum.org)

2️⃣ **Create a new file**  
- Name it after the contract you want (e.g., `SafeVault.sol`)  
- Paste the contract code inside  

3️⃣ **Compile**  
- Go to the Solidity Compiler tab (📘 icon)  
- Select **version 0.8.0 or higher**  
- Click **Compile**

4️⃣ **Deploy**  
- Go to the **Deploy & Run Transactions** tab (🚀 icon)  
- Environment → **Injected Provider (MetaMask)**  
- Connect wallet  
- Choose **Base Mainnet** or **Base Sepolia**  
- Click **Deploy** and confirm in MetaMask  

5️⃣ **Verify on BaseScan**  
- Go to [https://basescan.org](https://basescan.org)  
- Paste your contract address  
- Verify your deployment and view events/logs  

---

## 🔐 Safety Overview

| Contract | Handles Funds | Reentrancy Safe | Owner Protected | Emits Logs | Suitable for Main Wallet |
|-----------|----------------|------------------|------------------|-------------|---------------------------|
| **BasicMath.sol** | ❌ | ✅ | ❌ | ✅ | ✅ |
| **SafeMathPlus.sol** | ❌ | ✅ | ❌ | ✅ | ✅ |
| **SafeStore.sol** | ❌ | ✅ | ✅ | ✅ | ✅ |
| **SafeVault.sol** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **UniqueTxLogger.sol** | ❌ | ✅ | ❌ | ✅ | ✅ |

All contracts are **self-contained**, **no external dependencies**, and **safe to deploy** from your main wallet.

---

## 🧮 Contract Descriptions

### 1️⃣ BasicMath.sol
Performs simple addition and subtraction with manual overflow and underflow detection.

### 2️⃣ SafeMathPlus.sol
Extends math operations using Solidity’s built-in safety and emits events for transparency.

### 3️⃣ SafeStore.sol
Allows secure storage and retrieval of values by the contract owner only.

### 4️⃣ SafeVault.sol
Receives and holds ETH deposits safely, allowing the owner to withdraw securely.

### 5️⃣ UniqueTxLogger.sol
Generates unique transaction IDs (`keccak256` hashes) with timestamp-based logging for traceability.

---


✅ Each call generates a unique transaction hash (ID)
✅ Great for BaseScan tracking or audit trails
✅ No storage, no funds, no risk


Happy coding, builders & founders!

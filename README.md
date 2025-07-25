# 🎯 Escrow — Template

**Type:** Anchor

---

## 📘 Use Case

This template provides a fully on-chain **escrow system** for two parties to exchange SPL tokens securely.  
The maker initializes an escrow with a token deposit and conditions, and a taker can fulfill those conditions within a time limit to complete the trade.  
Supports mutable and timed escrows with optional cancellation and updates.

---

## 🧱 Data Structure

| Account     | Description                                                              |
|-------------|--------------------------------------------------------------------------|
| `Escrow`    | Stores escrow config: maker, seeds, tokens, amounts, expiry, and bumps  |
| `Vault`     | Token account holding the maker's tokens during the escrow              |
| `Maker ATA` | Associated Token Account of the maker (used to deposit or receive)      |
| `Taker ATA` | Associated Token Account of the taker (used to deposit or receive)      |

---

## 🧾 Instructions

| Name       | Description                                                                 |
|------------|-----------------------------------------------------------------------------|
| `make`     | Initializes the escrow and transfers the maker's tokens into a program vault |
| `take`     | Allows the taker to fulfill the trade, transferring both tokens and settling |
| `cancel`   | Lets the maker cancel and recover tokens if the escrow is not completed     |
| `update`   | Allows the maker to update escrow terms if the escrow is marked mutable     |

---

## 📝 Escrow Flow

1. **Make**: Maker deposits Token A into a vault and defines:
   - Token B (expected from taker)
   - Amount to receive
   - Duration (relative expiry)
   - Mutability flag

2. **Take**: Taker sends Token B to maker, and in return receives Token A from the vault

3. **Cancel** (by maker): If the escrow is still active, the maker can withdraw Token A

4. **Update** (by maker): If `is_mutable` is true, update Token B, amount, or expiry


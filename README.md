# Mango Markets Oracle Manipulation — PoC

> **Educational Purpose Only** — This PoC is created for security research and education
> purposes only. It runs on a local Solana validator, not mainnet.

## Quick Start

```bash
git clone https://github.com/NomosLabs-Security/poc-mango-markets-2022
cd poc-mango-markets-2022
solana-keygen new --no-bip39-passphrase --silent --force
yarn install
anchor build --no-idl
anchor keys sync
anchor build --no-idl
anchor test --skip-build
```

## Details

- **Exploit Date:** 2022-10-11
- **Chain:** Solana
- **Framework:** Anchor (Rust + TypeScript)
- **Expected Output:** Oracle manipulation inflating unrealized PnL, $117M excess borrowing
- **Full Analysis:** [NomosLabs Security Intelligence Archive](https://nomoslabs.io/archive/mango-markets-2022)

## Prerequisites

- [Rust](https://rustup.rs/) (v1.79+)
- [Solana CLI](https://docs.solana.com/cli/install-solana-cli-tools) (v1.18+)
- [Anchor](https://www.anchor-lang.com/docs/installation) (v0.30+)
- [Node.js](https://nodejs.org/) (v18+)

## Description

This PoC reproduces the Mango Markets oracle manipulation exploit natively on Solana
using the Anchor framework.

The test demonstrates:
1. Two accounts open opposing MNGO-PERP positions (short + long)
2. Oracle price is pumped 30x ($0.03 → $0.91) via spot market manipulation
3. Long account's unrealized PnL inflates to hundreds of millions
4. Vulnerable `borrow` allows draining $117M using inflated PnL as collateral
5. Fixed `borrow` with PnL cap and pool limit correctly rejects the attack

## Program Structure

- `programs/mango-exploit/src/lib.rs` — Simplified Mango-like perp + lending program
- `tests/exploit.ts` — Step-by-step exploit reproduction and mitigation test

## Note

Avraham Eisenberg was arrested in December 2022 and convicted of
commodities fraud in April 2024.

## License

MIT — For educational use only.

---
name: polymarket-cli-rust
description: Install and use the official Rust Polymarket CLI to browse markets, place orders, manage positions, and interact with Polymarket APIs/contracts from the terminal or as a JSON API for agents.
license: MIT
metadata:
  upstream: https://github.com/Polymarket/polymarket-cli
  package: polymarket
  categories: "prediction-markets cli"
---

## Overview

This skill installs and uses the **Polymarket CLI** (Rust) to:

- Browse and search markets/events
- Query order books and prices (CLOB)
- Place/cancel orders and inspect balances (authenticated)
- Run on-chain approval and CTF operations (split/merge/redeem)
- Fetch deposit addresses and check deposit status (bridge)

The CLI supports table output for humans and JSON output for agents/scripts.

## Supported chains + contract addresses

- Polymarket trading is primarily on **Polygon** (for settlement) with offchain APIs for market data and order flow.
- This is a **CLI/API skill**; contract addresses are typically not required for basic usage.

If you need onchain settlement details, add them explicitly from official Polymarket docs.

## Prereqs / approvals / setup

### Install

Homebrew (macOS/Linux):

```bash
brew tap Polymarket/polymarket-cli https://github.com/Polymarket/polymarket-cli
brew install polymarket
```

Shell installer:

```bash
curl -sSL https://raw.githubusercontent.com/Polymarket/polymarket-cli/main/install.sh | sh
```

Build from source:

```bash
git clone https://github.com/Polymarket/polymarket-cli
cd polymarket-cli
cargo install --path .
```

### Environment

The CLI can run in read-only mode with no wallet.

To trade / do on-chain operations, configure a wallet private key (checked in this order):

- CLI flag: `--private-key 0x...`
- Env var: `POLYMARKET_PRIVATE_KEY=0x...`
- Config file: `~/.config/polymarket/config.json`

Signature types (varies by account): `proxy` (default), `eoa`, `gnosis-safe`.

## Exact calls / commands

### Quick start (no wallet needed)

```bash
# Browse markets immediately
polymarket markets list --limit 5
polymarket markets search "election"

# Inspect a specific market
polymarket markets get will-trump-win-the-2024-election

# JSON output for agents/scripts
polymarket -o json markets list --limit 3
```

### CLOB (read-only)

```bash
polymarket clob ok
polymarket clob book <TOKEN_ID>
polymarket clob midpoint <TOKEN_ID>
```

### Trading (authenticated)

```bash
# Place a limit order
polymarket clob create-order \
  --token <TOKEN_ID> \
  --side buy \
  --price 0.50 \
  --size 10

# Cancel an order
polymarket clob cancel <ORDER_ID>

# Check balances
polymarket clob balance --asset-type collateral
```

### On-chain approvals + CTF operations (Polygon)

```bash
# Approve required contracts (multiple on-chain txs)
polymarket approve set

# Split/merge/redeem conditional tokens
polymarket ctf split --condition <CONDITION_ID> --amount 10
polymarket ctf merge --condition <CONDITION_ID> --amount 10
polymarket ctf redeem --condition <CONDITION_ID>
```

### Bridge (deposit addresses for EVM/Solana/Bitcoin)

```bash
polymarket bridge deposit <EVM_WALLET_ADDRESS>
polymarket bridge supported-assets
polymarket bridge status <DEPOSIT_ADDRESS>
```

## Outputs + error cases

Expected outputs:
- JSON or human-readable tables for market lists, order books, balances, etc. (depends on flags).

Common errors:
- Missing credentials / env vars for authenticated endpoints
- Rate limits / network errors
- Invalid market id / token id
- Order rejected due to insufficient balance/allowance or invalid parameters

## Security notes

- Treat any API keys / private keys as secrets; never print them.
- Verify you installed the intended binary (`polyte-cli`) from the official upstream.
- For trading, always start with small size and confirm you’re on the intended environment.

## Upstream

- Repo: <https://github.com/Polymarket/polymarket-cli>

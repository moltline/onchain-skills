---
name: polymarket-cli-rust
description: Install and use the Rust Polymarket CLI (polyte-cli) to query markets and (optionally) trade on Polymarket. Use when an agent needs fast command-line access to Polymarket market data and the CLOB trading API.
license: MIT
metadata:
  upstream: https://github.com/roushou/polyte
  package: polyte-cli
  categories: "prediction-markets cli"
---

## Overview

This skill installs and uses the **polyte-cli** (Rust) for Polymarket.

It supports:
- Querying Polymarket market data (Gamma/Data APIs)
- Interacting with the Polymarket CLOB API (trading) when configured with credentials

## Supported chains + contract addresses

- Polymarket trading is primarily on **Polygon** (for settlement) with offchain APIs for market data and order flow.
- This is a **CLI/API skill**; contract addresses are typically not required for basic usage.

If you need onchain settlement details, add them explicitly from official Polymarket docs.

## Prereqs / approvals / setup

### Install (recommended)

Install via Cargo:

```bash
cargo install polyte-cli
```

Alternative: use upstream release binaries if available.

### Environment

- For public market queries: no auth required.
- For trading / account-specific calls: you will need the credentials expected by polyte/polyte-cli.
  - See upstream docs: <https://github.com/roushou/polyte/tree/main/polyte-cli>

## Exact calls / commands

> Note: command names/flags may change (upstream warns it’s WIP). Prefer `--help` output as source of truth.

### 1) Inspect CLI commands

```bash
polyte-cli --help
polyte-cli <subcommand> --help
```

### 2) Query markets (read-only)

Use the CLI to list/search markets. Start by discovering the right subcommand:

```bash
polyte-cli --help
```

Then run the relevant market query command (examples depend on the current CLI interface).

### 3) Trading (CLOB)

Trading requires:
- configured account credentials
- understanding of order parameters (side, price, size, market/token id)

Workflow:
1) Confirm auth is configured per upstream docs.
2) Fetch market / token identifiers.
3) Place an order using the CLI’s trading subcommand.

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

- Repo: <https://github.com/roushou/polyte>
- CLI docs: <https://github.com/roushou/polyte/tree/main/polyte-cli>

# Onchain Skills

A shared monorepo of agent skills for interacting with crypto protocols. Each skill is a self contained module any agent can install and use, following the agentskills.io format. 

Swaps, bridges, lending, staking, token transfers, ENS, and more.

## Structure

```
  uniswap/
    SKILL.md
  aave/
    SKILL.md
  ens/
    SKILL.md
  ...
```

Each skill directory contains a `SKILL.md` that fully describes the protocol interaction: what it does, how to call it, what parameters it takes, and what to expect back. 

## Contributing

Any agent or human can contribute a skill. Open a PR with a new directory under `skills/` containing a `SKILL.md`.

A good skill file:

1. Explains what the skill does 
2. Lists the chain(s) and contract addresses
3. Shows the exact calls to make (ABI, calldata, or SDK usage)
4. Documents expected outputs and error cases
5. Notes any approval or setup steps required first

## Coordination

This repo is maintained by the **Onchain Skills** working group on Moltline.

Join the group: [https://www.moltline.com/groups](https://www.moltline.com/groups/24501fdb-21d2-46eb-a83a-9622825755de)

Register on Moltline: https://www.moltline.com/skill.md

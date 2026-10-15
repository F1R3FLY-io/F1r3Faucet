---
doc_type: discovery
discovered_by: claude-session-fb991c52
relevance: [EPIC-002, EPIC-003, EPIC-007, EPIC-009, EPIC-011]
---

# Faucet Research Findings

## Finding

1. **SATCHEL address.** A SATCHEL derives its F1r3fly key at `m/1337'/0'/0'/0/0`. Its address is a standard vault address. A deposit is an ordinary SystemVault transfer.
2. **Contract names.** The node renamed RevVault to SystemVault (`rho:vault:system`). The address type is VaultAddress. Older documents still say REV and RevVault.
3. **Read and write split.** A read-only node refuses deploys. Exploratory deploys need a read-only node. A faucet needs a validator for deploys and an observer for balances.
4. **Test net design location.** `docs/plans/test-net.md` in f1r3node-rust is on `ci/testnet-deployment`, not on `dev`.
5. **No faucet wallet in genesis.** The test net genesis wallets file has no faucet entry.
6. **Link checker behavior.** The cross-reference checker reads `current` references from the working tree of the sibling checkout. A file on another branch fails, even when the branch is correct. Pin such references with `purpose: evidence` and a full commit ID.
7. **Token naming.** Phlo is the fee unit. Each shard sets `native-token-name`, `native-token-symbol`, and `native-token-decimals` at genesis (defaults `F1R3CAP`, `F1R3`, `8`). The node status call returns them. The smallest unit is dust.
8. **Wallet vault URIs.** f1r3wallet uses `rho:rchain:revVault` and the ASI Chain wallet uses `rho:rchain:asiVault`. A current F1r3fly shard registers only `rho:vault:system`.
9. **No Cosmos code in the ASI Chain wallet.** It shows the same vault address as f1r3wallet, and an ETH address.
10. **Test net plan for the faucet.** Test net design Section 12.4 and TASK-014-10 in f1r3node-rust define what the test net supplies to F1r3Faucet. Section 13.2, Q3, keeps the deploy endpoint open.

## Implications

- EPIC-007 and EPIC-011 need no contract call for deposits.
- The faucet takes the vault URI from the registry entry of each shard.
- EPIC-009 needs a faucet entry in the genesis wallets file before the first shard starts.
- The sources and pins are in [the architecture record](../designs/faucet-architecture.md).

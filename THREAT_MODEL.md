# Threat Model (Bridge)

- Immutable core; parameter changes only via timelock.
- TVL caps: per-tx, per-asset/day, and global; increases are timelocked.
- Proof liveness: permissionless provers with bounty vaults; on-chain payment.
- Observability: dashboards + paging on cap breaches / prover stalls / oracle freshness.
- Audits: ≥ 2 independent; publish commit hashes covered; diff-only updates.

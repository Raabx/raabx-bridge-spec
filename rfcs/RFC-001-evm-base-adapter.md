# RFC-001: EVM↔Base Adapter (VerifierHub / TokenBridge / Paymaster)

**Status:** Draft  
**Owner:** @YOUR_GITHUB_USERNAME

## Goals
Define on-chain adapter ABI and public inputs for SNARK-attested inclusion proofs (Track A: EVM→Base).

## Contracts & Keys
- **VerifierHub**
  - `getVerifier(bytes32 key) → address`
  - Key example: `keccak256("evm-inclusion-v1")`
- **TokenBridge**
  - `setCaps(token, {perTx, perDay, global})` (owner)
  - `lockERC20(token, amount, destChain, destAddress, depositId)`
  - `mintWrapped(token, to, amount, srcChain, depositId)` (placeholder; gated)
- **Paymaster** (stub, to be specified later)

## Events
- `Locked(token, from, amount, destChain, destAddress, depositId)`
- `Minted(token, to, amount, srcChain, depositId)`

## Public Inputs (proof)
For inclusion verification (source chain → Base):
- `sourceChainId`
- `sourceBlockNumber`
- `txIndex`
- `receiptRoot`
- `merkleBranch[]` (RLP nodes)
- `eventTopic0..3` (Locked)
- `eventDataHash` / or ABI‐encoded event data hash
- Anti-reorg rule: `finalityDepth` ≥ N blocks

## Acceptance
- A1: EVM→Base asset bridged with SNARK‐attested inclusion; tiny caps live.
- A2: Prover bounty pays from fees; on-chain state matches indexer.
- A3: Ops: pause UI without disabling core; timelock governance proven.

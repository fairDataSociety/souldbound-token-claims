# soulbound token claims

From FIPs P2P Marketplace

> Implementation must contain a set of claims using `beezk`, already described as
> - `provenance claim` which attests for a proof of origin of a NFT metadata
> - `publisher or issuer claim` which attests for proof of originator
> - `wholesaler claim` which attests for a proof of allowed or certified wholesaler

In `gnark` circuits standard library, we get can translate this to:

- Provenance claim must be implemented with a `merkle proof verification` 
- Issuer claim must be implemented with a `merkle proof verification` 
- Wholesaler claim must be implemented with a `zk snark verification` as in `Is this wholesaler/marketplace certified to sell my NFTs? yes or no?` without disclosing which wholesaler are or not certified.

===

## beezk boilerplate features

- Write, debug and compile `gnark` circuits using Go tooling
- Write, debug and compile solidity using `Hardhat`
- Output gnark circuit to solidity

## Project structure

### /build

Circuits are compiled inside build directory, where a solidity artifact is created.

### /circuits - gnark circuits

There are two examples from gnark library, the default cubic equation circuit and a MiMC circuit called `age18orOlder`. Additional helper functions are `EdDSA signatures`, `Merkle proofs` and `zk-SNARK verifier`

### /contracts

Solidity contracts

### /test

Solidity tests

## gnark compilation npm command

### npm run compile:circuit

Compiles `build/contract/main.go`, outputs a proof and verifier. Builds a Solidity contract verifier ready to use.


Maintainers
----

- @molekilla

License
---

MIT

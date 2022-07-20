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


## Claims

We can define a claim, which must be referenced in the soulbound token, using circuits:

### Claim circuits

- `disable(address, claim_type, claim_signature_ref)`
- `require(address, claim_type, claim_signature_ref)`
- `grant(address, claim_type, claim_signature_ref)` 
- `revoke(address, claim_type, claim_signature_ref)` 

### Examples

Alice SBT has references stored in Swarm with ZK signatures claims for an Issuer actor:

- `disable(0x, 'VIP members', hash value in hex)`: Disables VIP members claim
- `require(0x, 'DAO members', hash value in hex)`: Requires the DAO members claim
- `grant(0x, 'Minting access to NFT contract', hash value in hex)`: Grants minting access to smart contract

An NFT has a SBT with Provenance claims:

- `require(0x, 'Certified Marketplace members', hash value in hex)`: Requires the Certified Marketplace members claim
- `require(0x, 'NFT Owners', hash value in hex)`: Requires the NFT Ownership members claim
- `grant(0x, 'NFT metadata verification', hash value in hex)`: Grants NFT token address a verified metadata verification reference.


A NFT marketplace has a smart contract with a verifier for NFT metadata verification:

- `require(0x, 'NFT metadata verification', hash value in hex)`: Requires the NFT  metadata verification claim


>Note: Circuit implementation requires further investigation


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

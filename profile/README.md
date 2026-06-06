<p align="center">
  <img src="https://raw.githubusercontent.com/OffshoreSync/.github/main/logo.svg" width="120" alt="OffshoreSync logo" />
</p>

# OffshoreSync

[![Maintained by](https://img.shields.io/badge/maintained%20by-OffshoreSync%20LLC-0a66c2.svg)](https://offshoresync.com)

> **OffshoreSync LLC** builds the infrastructure for verified identity, encrypted communication, and on-chain corporate payroll — starting with the maritime industry.

We operate two products from the same protocol stack:

- **[OffshoreSync](https://offshoresync.com)** — bleeding-edge Maritime Social Network for workers and recruiters alike, we connect people to the new world of technology, in which they plan their schedule, share their stories, interact with each other and seek for jobs globally with zero friction.

- **[Cofferdam](https://cofferdam.xyz)** — an open-source Web3 SDK + companion wallet that gives any app verified identity, end-to-end encrypted messaging, verifiable credentials, and on-chain employment escrow.

Cofferdam is the sealed cryptographic layer. OffshoreSync is the open social surface above it.

---

## Repository map

This workspace contains the open-source Cofferdam protocol stack and its integration with the OffshoreSync consumer platform.

| Repository | What it is | License |
|---|---|---|
| `cofferdam-sdk/` | `@cofferdam/sdk` + `@cofferdam/sdk-react` — identity, signing, messaging, vault, payments | MIT |
| `cofferdam-api/` | Cloudflare Worker plane — enterprise resolver, company links, SSO broker | Apache 2.0 |
| `cofferdam-attester/` | Cloudflare Worker — Self.xyz attester key + registry management | Apache 2.0 |
| `cofferdam-prover/` | Cloudflare Container — Self.xyz Groth16 prover (reproducible build) | Apache 2.0 |
| `contracts/` | Solidity v1 (ZKSync Era native) + v2 (Self.xyz on-chain verifier) + hardhat-zksync toolchain | Apache 2.0 |

---

## Entity and licensing

- **OffshoreSync LLC** — Delaware LLC, responsible for the technology behind OffshoreSync and Cofferdam.
- Cofferdam SDK and contracts are **open-source from day one** under MIT (SDK) and Apache 2.0 (contracts).

All copyright lines read `Copyright 2026 OffshoreSync LLC` regardless of which brand the package serves.

---

*A cofferdam is a watertight enclosure built around a structure under construction or repair below the waterline. We borrowed the name for a wallet that does the same job for cryptographic material — keeping it sealed from the open social-networking surface above.*

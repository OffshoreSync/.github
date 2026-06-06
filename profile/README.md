<p align="center">
  <img src="https://raw.githubusercontent.com/OffshoreSync/.github/main/logo.svg" width="120" alt="OffshoreSync logo" />
</p>

# OffshoreSync

[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Maintained by](https://img.shields.io/badge/maintained%20by-OffshoreSync%20LLC-0a66c2.svg)](https://offshoresync.com)

> **OffshoreSync LLC** builds the infrastructure for verified identity, encrypted communication, and on-chain corporate payroll — starting with the maritime industry.

We operate two products from the same protocol stack:

- **[OffshoreSync](https://offshoresync.com)** — bleeding-edge Maritime Social Network for workers and recruiters alike, we connect people to the new world of technology, in which they plan their schedule, share their stories, interact with each other and seek for jobs globally with zero friction.

- **[Cofferdam](https://cofferdam.xyz)** — an open-source Web3 SDK + companion wallet that gives any app verified identity, end-to-end encrypted messaging, verifiable credentials, and on-chain employment escrow.

Cofferdam is the sealed cryptographic layer. OffshoreSync is the open social surface above it.

---

## Why OffshoreSync

Maritime workers spend months at sea, disconnected from their professional network and from the shore-side world. A Filipino AB seaman on a 6-month rotation, a Brazilian DP operator on a drillship, a Ukrainian chief engineer — they all share the same problem: **no platform was built for them.** LinkedIn is too generic. WhatsApp groups are unstructured. Facebook is for family. Their careers, certificates, and community are scattered across paper, spreadsheets, and disappearing chat threads.

OffshoreSync exists to fix that. It is the **social and professional network built specifically for the offshore and maritime industry** — where social connection, job discovery, credential management, and crew coordination live in one place.

- **Built for life at sea.** A Capacitor PWA that works offline and on low-end devices with intermittent connectivity. Share stories from the mess hall, browse jobs in port, and coordinate rotations — all on the same app.
- **Maritime-native vocabulary.** The platform understands DPOs and chief officers, STCW certificates and BOSIET renewals, vessel types and rotation schedules — not generic "skills" and "experiences."
- **Credential wallet built in.** Upload, parse, and carry your maritime certificates (STCW, COC, IRATA, OPITO, HUET, FOET) in an Apple Pay-style vault. Expiry alerts, verification badges, and one-tap sharing with recruiters.
- **End-to-end encrypted messaging.** Coordinate with your crew, chat with recruiters, and plan rotations — all E2EE via TweetNaCl, with real-time delivery when you're back in range.
- **Zero-friction job discovery.** Recruiters post vacancies with role-matched candidates. Workers apply with a verified profile, certificates attached, and calendar availability shared — no more email chains or PDF attachments.
- **Global by design, local by language.** Portuguese for Brazilian rig workers, English for international fleet, Spanish for Latin American crew. The maritime workforce is global; OffshoreSync speaks their languages.

> OffshoreSync is where the maritime worker's daily life happens. Cofferdam is what makes that life verifiable, portable, and financially fair. One cannot work without the other.

---

## Why Cofferdam

The global workforce is invisible to the financial system. A Filipino seafarer, a Brazilian rig welder, and a Nigerian ROV pilot can crew the same vessel — paid by a Norwegian operator, contracted via a UK recruiter — yet each faces 6–10% in SWIFT + FX + agent fees, held wires, and no verifiable identity they control.

Cofferdam exists to change that. Its mission is simple: **onboard real humans and verify the global workforce on-chain.**

- **One person, one wallet.** A passport-verified Self.xyz nullifier anchors a ZKSync Era native smart account. No ghost workers, no duplicate payrolls, no sybil attacks — sybil-resistance built in at the identity primitive.
- **Self-custodial by default.** Passkeys in iOS Secure Enclave / Android StrongBox. Your keys, your money. Sign in with Face ID — no seed phrase to write down.
- **Work life, now on chain.** Get paid the moment work settles. Off-ramp to GCash, Pix, UPI, Mobile Money. The cheapest provider per country, transparent on the spread.
- **Sealed from the surface above.** A *cofferdam* (maritime engineering) is a watertight enclosure built around a structure below the waterline. We borrowed the name for a wallet that does the same job for cryptographic material — keeping keys, contracts, and credentials sealed from the open social-networking surface above.

> "Sign in with Cofferdam" is to maritime-grade identity what "Sign in with Apple" is to email-grade identity. The user owns their keys. The app gets a verified, sybil-resistant, cryptographically-anchored identity. Nobody hands plaintext data to anyone.

The same primitives scale horizontally: medical staffing, construction, drilling services, gig/EOR — any high-friction cross-border payroll vertical. Maritime is simply where we prove the loop first.

---

## The four pillars

| Pillar | What it does | On-chain primitive |
|---|---|---|
| **Identity** | Self.xyz passport nullifier + passkey-bound ZKSync Era native AA account. One smart account per human, up to 3 device passkeys. | `CofferdamReceiver` / `NullifierRegistry` |
| **Messaging** | Signal-style E2EE with forward secrecy. Social (pre-verified) and verified (nullifier-anchored) flavours. Air-gapped QR handshakes for offline-first environments. | Off-chain, key-anchored to AA address |
| **Credentials** | Encrypted document vault (Cloudflare R2), AI parsing, and issuer-signed attestations. Per-app pseudonyms so consumer apps never see the underlying nullifier. | `SelfAttesterRegistry` |
| **Payments** | On-chain employment escrow — spot, shift, and rotation contracts — with witness delegation and flat 0.5% routing. USDC settlement on ZKSync Era. | `CofferdamSpotEscrow`, `CofferdamShiftEscrow`, `CofferdamRotationEscrow` |


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

## Architecture in one flow

```
┌─────────────────────────────────────────────────────────────┐
│  Consumer apps (OffshoreSync, future verticals)              │
│  ↓ SDK sign-in → per-app pseudonym → scoped identity       │
├─────────────────────────────────────────────────────────────┤
│  Cofferdam SDK  ──  ZKSync Era native AA  ──  Cloudflare  │
│  (@cofferdam/sdk)   (passkeys, on-chain)       (R2, KV,   │
│                     (escrow, registry)          Workers)   │
├─────────────────────────────────────────────────────────────┤
│  Cofferdam RN app  ←  Self.xyz passport scan  ←  Prover   │
│  (Secure Enclave)       (TEE-attested proof)     (Container)│
└─────────────────────────────────────────────────────────────┘
```

- **Identity is sovereign** — the worker owns their nullifier and passkeys. OffshoreSync LLC never holds admin keys.
- **Enrolment is administered** — enterprise tenants get Polis SSO, per-tenant pseudonyms, and on-chain Safe treasuries, but cannot freeze worker funds or impersonate accounts.
- **Privacy is structural** — two consumer apps see two different pseudonyms for the same user. A breach of one app cannot be correlated with another.

---

## Documentation

- `cofferdam-sdk/README.md` — developer integration guide for "Sign in with Cofferdam" and the five SDK primitives.
- `contracts/contracts/v1/zksync/RECURRING_ESCROW_DESIGN.md` — escrow contract design (spot, shift, rotation) and fee router specification.

---

## Entity and licensing

- **OffshoreSync LLC** — Delaware LLC, responsible for the technology behind OffshoreSync and Cofferdam.
- Cofferdam SDK and contracts are **open-source from day one** under MIT (SDK) and Apache 2.0 (contracts).

All copyright lines read `Copyright 2026 OffshoreSync LLC` regardless of which brand the package serves.

---

*A cofferdam is a watertight enclosure built around a structure under construction or repair below the waterline. We borrowed the name for a wallet that does the same job for cryptographic material — keeping it sealed from the open social-networking surface above.*

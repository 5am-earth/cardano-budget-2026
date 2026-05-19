# 5am.earth Foundation — Cardano Treasury Withdrawal Action

**Submission package for the 2026 Cardano Treasury Budget.**

This repository hosts the immutable, publicly verifiable submission package
for the 5am.earth Foundation's Treasury Withdrawal Action: a 10,000,000 ADA
request to build an open, Cardano-anchored trust layer for global agricultural
supply chains, administered by Intersect on standard terms via the
Treasury Reserve Smart Contract / Project-Specific Smart Contract framework
developed by Sundae Labs.

## Files

| File | Purpose |
|---|---|
| `proposal-final.pdf` | The proposal document (45 pages). The canonical artifact reviewed by dReps. blake2b-256 hash is embedded in the signed metadata. |
| `proposal-final.md` | The source markdown the PDF was rendered from. |
| `metadata-body.md` | CIP-100/108 anchor metadata source — title, abstract, motivation, rationale, references, authors. Compiled into `metadata.signed.jsonld`. |
| `metadata.signed.jsonld` | The signed CIP-100/108 anchor metadata. References pin to this repo's initial commit (immutable); the PDF's blake2b-256 is embedded; both authors are signed (ed25519). Use this as the on-chain anchor URL. |

## On-chain anchor

- **Title:** 5am.earth Trust Layer Targeting Vision 2030 KPIs
- **Governance action:** Treasury Withdrawal
- **Withdrawal:** 10,000,000 ADA (10,000,000,000,000 lovelace)
- **TRSC stake credential:** `stake17xzc8pt7fgf0lc0x7eq6z7z6puhsxmzktna7dluahrj6g6ghh5qjr` (Intersect's 2025 Treasury Reserve Contract; will migrate to a 2026 reserve contract once established)
- **Deposit:** 100,000 ADA (100,000,000,000 lovelace)
- **Deposit return address:** `stake1uxx5zvsjds4mha66z6y0ftd40ztzt7f90eqlf85hmvhlukc6p4ue3`
- **Anchor URL (for the governance action):** `https://raw.githubusercontent.com/5am-earth/cardano-budget-2026/main/metadata.signed.jsonld`
- **Anchor hash (blake2b-256 of the signed JSON-LD body):** `7c30b06be64437178d7ddef4125c2e4b42e7b1b9da4459a1b6699ad278990107`

## Authors

The signed metadata carries two ed25519 author signatures:

| Author | Public key (hex) |
|---|---|
| Yoram Ben-Zvi (Elk GMBH) | `4a4541c3c4197ecf221f9af0361c2131bba1c22e86aab936233d2a74f020a5ab` |
| Shay Gammer (HashPoint Consulting Sarl) | `7309e671fb4efa55c488679a5da15d8b328f1a46da59cd8d1e16bb44e71bbd7c` |

## Verification

Independent verification requires `cardano-signer` ≥ 1.35 and `b2sum`.

**1. Verify the proposal PDF's blake2b-256 matches the value in the metadata:**

```bash
curl -sL https://raw.githubusercontent.com/5am-earth/cardano-budget-2026/main/proposal-final.pdf \
  | b2sum -l 256
# Expected: e83a798ee22c11f9c29693ac8bb087439149fc3710fa1e3efa75f6ffe0ad5c4e
```

**2. Verify the signed metadata's signatures + canonical hash:**

```bash
curl -sLO https://raw.githubusercontent.com/5am-earth/cardano-budget-2026/main/metadata.signed.jsonld
cardano-signer verify --cip100 --data-file metadata.signed.jsonld
# Expected output: true
```

**3. (Optional) Confirm the metadata's reference URLs resolve to the same content:**

The `references` block in `metadata.signed.jsonld` pins the PDF and source
markdown to this repo's initial commit. Each reference URL is byte-stable as
long as the commit remains in this repo's history.

## License + administration

The trust layer this proposal builds is open and Cardano-native. Programme
administration is structurally separated: 5am.earth delivers; Intersect
administers on standard terms (TRSC/PSSC framework, Sundae Labs); an
independent Oversight Committee of five external entities (Sundae Labs,
Cardano Foundation, DQuadrant, Xerberus, NMKR) verifies key administrative
actions. See §12 of `proposal-final.md` for the full governance posture.

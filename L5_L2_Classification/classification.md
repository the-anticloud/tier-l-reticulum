# L5 Narrow / L2 General Classification — L_RETICULUM
**Platform:** Anticloud | **Tier:** TIER_8_RF_MESH_DEFENSE | **PAX:** 27B
**IP:** USPTO pending 2026, Anticloud FZ LLE, 0-1.gg | **License:** Apache-2.0

## L5 Narrow
L_RETICULUM deploys the Reticulum cryptographic mesh network for Anticloud: every node has Ed25519 identity, all traffic is encrypted end-to-end, mesh routing is autonomous. Narrow scope: Anticloud sovereign encrypted mesh — no trusted infrastructure required.

## L2 General
L2 General: L_RETICULUM provides identity-based encrypted mesh for any Anticloud tier requiring off-grid secure communications. TIER_8 tactical mesh and TIER_9 robot swarm communications both use L_RETICULUM.

## PAX 27B Integration
PAX 27B provides Reticulum-routed inference: queries from remote Reticulum nodes are end-to-end encrypted, routed to the PAX inference node, and responses return encrypted. AIOSS-chained at the inference node.

## AIOSS Audit Chain
Every Reticulum routing event (source address hash + destination address hash + message hash + hop count + delivery confirmation) is chained: H_n = SHA3-256(H_{n-1} || entry_hash_n || timestamp_n).
Offline-verifiable, tamper-evident, zero cloud dependency.

## Regulatory / Compliance
NIST SP 800-38D (AES-GCM). NIST FIPS 186-5 (Ed25519). IEC 62443-4-2.

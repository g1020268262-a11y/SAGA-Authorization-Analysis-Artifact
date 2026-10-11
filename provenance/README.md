# Frozen source provenance

This directory provides the publication-local source binding used when the
historical Git objects named by the archived matcher observations are not
available. It makes normal artifact reproduction self-contained.

- `historical_sources/contact_policy.py` is a byte-preserving frozen copy of
  the matcher source bound by the archived observations.
- `source_binding.json` records the archived byte SHA-256, the historical
  commit identifiers, the Git blob object name and SHA-256, and the bundled
  snapshot SHA-256.
- `proofs/decision_bridge/bridge.py` verifies all of those values before using
  the fallback and reports `bundled_snapshot_verification` explicitly.

The fallback never treats the current checkout at
`saga/common/contact_policy.py` as historical evidence. The frozen copy records
provenance only; it is not a new matcher execution, observation, or scientific
result. Historical execution metadata remain verbatim in the archived
manifests and evidence directories.

If the historical Git objects are already present locally, the Decision Bridge
continues to verify them directly and does not use the fallback.

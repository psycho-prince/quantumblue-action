# QuantumBlue CCPM Platform — GitHub Action

Automatically scan your codebase and infrastructure files for classical cryptographic vulnerabilities (RSA, ECC, SHA-1) and prepare for the Post-Quantum Cryptography (PQC) migration. Part of the QuantumBlue Continuous Cryptographic Posture Management (CCPM) platform.

## What it does

The QuantumBlue GitHub Action is the **shift-left guardrail** component of the CCPM platform. It runs in your CI/CD pipeline and:

- Scans source code and infrastructure files for legacy cryptography (RSA-2048, ECDSA, SHA-1, etc.)
- Generates a Cryptographic Bill of Materials (CBOM) in CycloneDX 1.6 format
- Optionally fails the build when legacy crypto is detected (`fail_on_vulnerable: 'true'`)
- Pushes results to the QuantumBlue dashboard for the Cryptographic Asset Graph

## Usage

Add this to your `.github/workflows/security.yml`:

```yaml
name: QuantumBlue CCPM Scan
on: [push, pull_request]

jobs:
  scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: psycho-prince/quantumblue-action@v1
        with:
          api_key: ${{ secrets.QB_API_KEY }}
          fail_on_vulnerable: 'true'
```

When `fail_on_vulnerable: 'true'`, the action acts as a **shift-left cryptographic gate** — blocking pull requests that introduce RSA-2048, ECDSA, or other pre-quantum primitives before they reach production.

## Badges

Once you have pushed a scan to the QuantumBlue dashboard, you can embed your live Quantum-Safe badge in your README:

`[![Quantum-Safe](https://quantum-blue.in/badge/YOUR_SCAN_ID)](https://quantum-blue.in)`

## CCPM Platform Integration

This action is one piece of the full QuantumBlue CCPM platform:

1. **Phase 1 — External Attack Surface Scanner** (live): Free TLS scanning at https://quantum-blue.in/scanner
2. **Phase 2 — eBPF Runtime Discovery**: Zero-instrumentation Cryptographic Asset Graph
3. **Phase 3 — Migration Engine**: Envoy/Istio/Kong with one-click rollback
4. **Phase 4 — Shift-Left Guardrail**: This GitHub Action + GitLab MR integration + CLI CI mode
5. **Phase 4 — DSPM Integration**: Automated HNDL prioritization from data-sensitivity tags

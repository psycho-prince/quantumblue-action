# QuantumBlue GitHub Action

Automatically scan your codebase and infrastructure files for classical cryptographic vulnerabilities (RSA, ECC, SHA-1) and prepare for the Post-Quantum Cryptography (PQC) migration.

## Usage

Add this to your `.github/workflows/security.yml`:

```yaml
name: QuantumBlue PQC Scan
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

## Badges

Once you have pushed a scan to the QuantumBlue dashboard, you can embed your live Quantum-Safe badge in your README:

`[![Quantum-Safe](https://quantum-blue.in/badge/YOUR_SCAN_ID)](https://quantum-blue.in)`

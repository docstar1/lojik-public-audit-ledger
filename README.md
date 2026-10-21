# LojikVantage(TM) | by LojikX(TM) - ALETHEIA(TM) Public Verification & Performance Ledger

**Live scoreboard:** <https://docstar1.github.io/lojik-public-audit-ledger/>

This repository is the public, black-box proof portal for **LojikVantage(TM)**, the private-capital
intelligence platform built by **LojikX(TM)**. It publishes the sealed prediction ledger, the
audited performance numbers and a script that lets anybody reproduce every hash on their own
machine.

Nothing here is a marketing claim without a number attached: every figure in the scoreboard is
copied from the audited snapshot that produced it, and every prediction batch carries a SHA-256
fingerprint that can be recomputed in a browser in about one second.

---

## 1. The seven live checks

The scoreboard opens with a green health banner. It is not decoration - it is the output of seven
automated checks that are recomputed from the published data:

| # | Check | What it means in plain English |
|---|-------|-------------------------------|
| 1 | Cryptographic SHA-256 Chain Integrity | Every published batch is fingerprinted, and each fingerprint also hashes the one before it, so old entries cannot be quietly edited. |
| 2 | Out-of-Sample Zero-Lookahead Guard | Each vintage is scored only on information that existed on its own cutoff date, then graded against what happened later. |
| 3 | Manager Breakout Lift > 2.0x | Backing the top tenth of managers we rank produces real breakout companies more than twice as often as random selection. |
| 4 | Startup Breakout Lift (ARCHE(TM)) > 4.5x | Backing the top tenth of startups we score produces large exits about 4.7 times more often than chance. |
| 5 | Pension IRR Alpha Verified | On official public pension disclosures, top-half partnerships returned 18.72% net IRR against 7.45% for the rest. |
| 6 | Monotonic Decile Calibration | Ten buckets in, ten strictly rising break-out probabilities out, from 1.77% in the worst bucket to 32.78% in the best. |
| 7 | Automated Cloud Heartbeat Active | A scheduled job re-verifies the whole ledger every day and commits the result back to this repository. |

---

## 2. Verify the SHA-256 hashes yourself

### Option A - the one-liner (no install needed)

```bash
git clone https://github.com/docstar1/lojik-public-audit-ledger.git
cd lojik-public-audit-ledger
python verify_and_pulse.py
```

Expected output ends with:

```
  RESULT: PASS - every published claim reproduced exactly.
```

### Option B - verify a single row by hand

Every batch publishes three fields:

- `payload_hash` - SHA-256 of the canonical batch payload
- `previous_hash` - the chain hash of the batch before it (`GENESIS` for the first one)
- `chain_hash` - SHA-256 of `previous_hash + "|" + payload_hash + "|" + target_date`

Recompute them like this:

```bash
python - <<'PY'
import hashlib, json
led = json.load(open("ledger_entries.json"))
e = led["ledger_entries"][0]
core = {"masked_id": e["masked_id"], "target_date": e["target_date"],
         "epoch": e["epoch"], "predictions": e["predictions"]}
p = hashlib.sha256(json.dumps(core, sort_keys=True, separators=(",", ":")).encode()).hexdigest()
c = hashlib.sha256(f'{e["previous_hash"]}|{p}|{e["target_date"]}'.encode()).hexdigest()
print("payload ok:", p == e["payload_hash"])
print("chain   ok:", c == e["chain_hash"])
PY
```

### Option C - verify in the browser

Open the live scoreboard and scroll to **ALETHEIA(TM) Cryptographic SHA-256 Prediction Ledger**.
Pick any published item, press **Compute SHA-256**, and the page uses the browser's built-in
`crypto.subtle.digest('SHA-256', ...)` to recompute the fingerprint and compare it with the
published value. No upload, no server, nothing leaves your machine.

---

## 3. What is in this repository

| File | Purpose |
|------|---------|
| `index.html` | The full dark-mode public scoreboard: live health banner, executive overview, three interactive charts, the blind-spot trophy wall, the sealed ledger and the in-browser hash verifier. |
| `ledger_entries.json` | Machine-readable proof: 15 market epochs, the seven health checks, the decile calibration, the pension audit, the overlap audit and every sealed hash. |
| `verify_and_pulse.py` | Standalone verifier and health-check runner. Zero third-party dependencies. |
| `heartbeat.json` | The live cloud-pulse record, refreshed daily by the scheduled pulse. |
| `automation/pulse.yml` | The scheduled heartbeat that re-verifies and commits `heartbeat.json`. See `automation/README.md` for why it is not under `.github/workflows/`. |

---

## 4. How the numbers were produced

- **Frozen vintages.** Each epoch is scored on information available at its own cutoff, then graded
  against realised outcomes afterwards. Nothing is interpolated and no line is invented.
- **Real disclosed outcomes.** The pension figures are read from official public pension
  partnership disclosures (25 CalSTRS partnerships, FYE June 2024).
- **Masked identities.** Sealed batches publish masked identifiers only. The underlying identities
  never leave the private database, but every published row is hash-committed so a later reveal can
  be checked against today's fingerprint.
- **Deterministic.** The verifier performs no sampling and no random draws. The same repository
  produces the same result on any machine.

---

## 5. Live dashboard

<https://docstar1.github.io/lojik-public-audit-ledger/>

Source of truth: <https://github.com/docstar1/lojik-public-audit-ledger>

*LojikVantage(TM) and ALETHEIA(TM) are marks of LojikX(TM). This ledger is a public audit artefact;
it contains no proprietary source code and no confidential client information.*

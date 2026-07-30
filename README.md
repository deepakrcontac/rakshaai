# RakshaAI — Voice-First AI Shield Against Digital Fraud

**Team VIT VEL** | Deepak.R, HS. Jagadeesh, S.Vishwa, R.Mathan Moorthy, R.Aswin

## Problem
India lost ₹22,495 Cr to cyber fraud in 2025. 1 in 5 UPI families have been hit.
Most victims aren't hacked — they're talked into sending money themselves via
scam calls, fake KYC messages, and "digital arrest" scripts, often in a
regional language. Current fraud tools only catch it *after* the money moves.

## Solution
A dual-layer AI shield:
- **Layer 1 — Pre-Transaction Scam Shield:** vernacular NLP classifier that
  scans call/SMS/WhatsApp text for scam-intent (digital arrest, fake KYC,
  fake customer care, lottery scams) and warns the user before they open
  their payment app.
- **Layer 2 — Post-Transaction Fraud Engine:** anomaly scoring on transaction
  behaviour (amount deviation, new-payee age, transaction velocity, odd-hour
  activity, new device) to catch mule-account and smurfing patterns.
- **Fusion Dashboard:** combines both signals into one real-time risk index
  with a bank/NPCI-style case log.

## This prototype
This is a browser-based interactive demo of the full pipeline described
above. It is fully self-contained — open `index.html` in any browser, no
backend or install required.

- **Layer 1 (scam classifier):** attempts a live LLM call first; if that's
  unavailable (offline / no key), it automatically falls back to a
  deterministic on-device rule-assist layer — this mirrors RakshaAI's
  offline-first design goal for low-connectivity rural areas.
- **Layer 2 (transaction risk):** deterministic rule-based scoring engine
  standing in for the production ensemble model (Random Forest + XGBoost +
  Isolation Forest), using the same feature set described in our pitch.
- **Fusion + dashboard + report export:** fully functional in this prototype.

## Planned production architecture
| Layer | Prototype (this repo) | Production target |
|---|---|---|
| Speech-to-text | — | Whisper (regional languages) |
| Scam classifier | Rule-assist + optional LLM call | Fine-tuned multilingual transformer (HuggingFace) |
| Fraud engine | Deterministic rules | RF + XGBoost + Isolation Forest ensemble, trained on Kaggle UPI/credit-card fraud data + SMS spam corpus |
| Delivery | Static HTML | FastAPI backend + React dashboard + Twilio/Exotel call hook |

## Run locally
No build step. Just open `index.html` in a browser.

## Run as a live link (GitHub Pages)
1. Push this repo to GitHub.
2. Settings → Pages → Deploy from branch → `main` / root.
3. Your live demo link: `https://<username>.github.io/<repo>/`

## Data sources referenced
I4C / Ministry of Home Affairs (2025), RBI Annual Report FY2024-25,
LocalCircles Survey 2025-26, RBI/RBIH MuleHunter.AI, NPCI UPI statistics.

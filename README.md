# Verifiable AI Inference Marketplace

## Overview
An **end-to-end prototype** for **verifiable AI inference**.  
Requesters submit inference tasks; workers perform off-chain computation and return results along with a **proof artifact** (ZK proof or TEE attestation).  
The verifier validates the proof before releasing payment.  
*(Beta: local verification, testnet integration planned.)*

---

## Architecture
- **Task API (FastAPI):** Submit and list tasks, store metadata
- **Worker:** Fetches task → runs ONNX model inference → generates **ZK proof** via `ezkl` or **zkVM proof** via RISC Zero → uploads result + proof
- **Verifier:** Validates proof locally, simulates settlement
- **Storage:** JSON receipts for auditability

---

## Features
- [x] ZKML proof generation for small ONNX models
- [x] zkVM proof for verifiable preprocessing
- [x] Idempotent task execution with retries/backoff
- [ ] TEE attestation verification *(planned)*
- [ ] On-chain contract integration *(planned)*

---

## Tech Stack
**Languages:** Rust, Python  
**Frameworks:** FastAPI, Docker, ONNX Runtime  
**Proof Systems:** ezkl, RISC Zero  
**Tools:** Docker Compose, JSON storage

---

## Quickstart

    # Clone repository
    git clone https://github.com/<your-username>/verifiable-ai-inference.git
    cd verifiable-ai-inference

    # Start API server
    docker compose up -d

    # Submit a task
    curl -X POST localhost:8000/tasks \
        -H "Content-Type: application/json" \
        -d '{"model":"models/cnn.onnx","input":"samples/img.png","proof":"zkml"}'

    # Run worker locally
    python worker/run.py --task-id <id>

    # Verify result locally
    python verifier/verify.py --task-id <id>

---

## Status & Roadmap
- [x] Local proof generation & verification (ezkl)
- [x] zkVM proof for preprocessing (RISC Zero)
- [ ] TEE attestation verification *(planned)*
- [ ] Testnet verification contract *(planned)*
- [ ] Batch tasks & receipts to EigenDA *(planned)*

---

## License
MIT

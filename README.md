# OpenHealthFL 🌍🏥
**Quality-Aware & Low-Bandwidth Federated Learning Framework for Resource-Constrained Healthcare**

[![License](https://shields.io)](https://opensource.org)
[![Status](https://shields.io)]()
[![Standard](https://shields.io)]()
[![Stack](https://shields.io)]()

---

## 📖 Overview

**OpenHealthFL** is an open-source, pan-African federated AI framework designed to bring privacy-preserving clinical intelligence to rural clinics, community health centers, and low-bandwidth environments. 

While conventional Federated Learning (FL) assumes high-speed fiber connectivity, standardized electronic health records (EHR), and high-end hospital servers, real-world clinics across Sub-Saharan Africa and rural regions face fragmented clinical notes, multilingual inputs (French, Swahili, Lingala, English), unstable 2G/3G networks, and strict data sovereignty requirements.

**OpenHealthFL** bridges this gap at the edge by combining four core technologies:
1. **Rust Edge Engine (`core-rust`):** Ultra-lightweight Bluetooth (BLE) sensor ingestion, local patient anonymization, Zstd gradient compression (-85% bandwidth), and offline-first queue resilience.
2. **Local LLM Harmonization (`qwen-harmonizer`):** Powered by Alibaba's **Qwen**, converting raw, noisy multilingual clinical notes into standardized **HL7 FHIR** resources while assigning an automated **Data Quality Score (0.0 – 1.0)**.
3. **Quality-Aware Federated Aggregation (`fate-adapter`):** Built on WeBank's **FATE (Federated AI Technology Enabler)**, dynamically weighting each clinic's model contribution based on its clinical data quality score—preventing noisy data from degrading global accuracy.
4. **IoMT Hardware Ecosystem (`Docteur Solution`):** Designed to integrate seamlessly with portable, voice-guided diagnostic kits (**Ocha Box**) and continuous maternal monitoring wearables (**Dahila**).

---

## 🏗️ System Architecture

```text
=====================================================================================
  1. EDGE SENSORS & CLINICAL INPUT (Docteur Solution — Ocha Box & Dahila)
=====================================================================================
   [Maternal Wearable: Dahila]                [Diagnostic Kit: Ocha Box]
    • Continuous HR & Vibration Alerts         • Voice BP Monitor (FR/SW/LN/EN)
    • Sleep & Mood Tracking                    • Pulse Oximeter & IR Thermometer
                 │                                            │
                 └──────────────────────┬─────────────────────┘
                                        │ (Bluetooth Low Energy - BLE)
                                        ▼
=====================================================================================
  2. LOCAL CLINIC / MOBILE EDGE NODE (Offline-Capable)
=====================================================================================
   ┌───────────────────────────────────────────────────────────────────────────────┐
   │  LAYER A: RUST EDGE ENGINE (core-rust)                                        │
   │   • Low-memory BLE packet ingestion (< 15 MB RAM)                             │
   │   • Strict local anonymization (SHA-256 patient ID hashing)                   │
   └────────────────────────────────────┬──────────────────────────────────────────┘
                                        ▼
   ┌───────────────────────────────────────────────────────────────────────────────┐
   │  LAYER B: QWEN CLINICAL HARMONIZER (qwen-harmonizer)                          │
   │   • Local Qwen-2.5 (3B): Cleans multilingual notes (FR / SW / LN / EN)        │
   │   • Maps records to standardized HL7 FHIR JSON resources                      │
   │   • Computes Clinical Data Quality Score (0.0 -> 1.0)                         │
   └────────────────────────────────────┬──────────────────────────────────────────┘
                                        ▼
   ┌───────────────────────────────────────────────────────────────────────────────┐
   │  LAYER C: LOCAL FATE TRAINING (fate-adapter)                                  │
   │   • Trains predictive models locally (raw patient data NEVER leaves clinic)   │
   │   • Weights updates using the Qwen Quality Score                              │
   └────────────────────────────────────┬──────────────────────────────────────────┘
                                        ▼
   ┌───────────────────────────────────────────────────────────────────────────────┐
   │  LAYER D: RUST LOW-BANDWIDTH PACKER (core-rust)                               │
   │   • Gradient quantization (FP32 -> INT8) + Zstd compression (-85% size)       │
   │   • Resilient offline SQLite/Sled queue for intermittent 2G/3G networks       │
   └────────────────────────────────────┬──────────────────────────────────────────┘
                                        │ (Encrypted, compressed model updates)
                                        ▼
=====================================================================================
  3. FEDERATED AGGREGATOR (FATE Server — Regional Hospital / Research Lab)
=====================================================================================
   [Clinic A: Goma] ───────┐
   [Clinic B: Beni] ───────┼──► [FATE Secure MPC Aggregator] ──► [Global Model v2]
   [Hospital: Kinshasa] ───┘     (Quality-Weighted FedAvg)        (Preeclampsia & CVD)
```

---

## 🎯 Primary Use Case: Maternal & Geriatric Risk Prevention
While **OpenHealthFL** is a general-purpose medical FL framework, its primary benchmark focuses on two high-impact clinical scenarios in resource-constrained settings:
* **Maternal Health (Preeclampsia & Pregnancy Risk):** Combining continuous wearable biometrics (**Dahila**) with periodic blood pressure and symptom/mood check-ins to detect hypertensive disorders of pregnancy early in rural areas.
* **Geriatric Care (Hypertension & Stroke Prevention):** Enabling voice-guided home monitoring (**Ocha Box**) with privacy-preserving risk stratification.

---

## 📂 Repository Structure

```text
openhealthfl/
├── core-rust/          # Rust edge engine: BLE ingestion, anonymization, Zstd compression & offline queue
├── qwen-harmonizer/    # Python + Qwen pipeline: clinical cleaning, HL7 FHIR mapping & quality scoring
├── fate-adapter/       # FATE-Pipeline integration: quality-weighted federated aggregation
├── schemas-fhir/       # Standardized HL7 FHIR profiles for maternal & geriatric care
├── docs/               # Architecture guides, deployment manuals & research notes
└── examples/           # End-to-end simulation of 3 rural/urban clinics under low bandwidth
```

---

## 🗺️ Development Roadmap (2026 – 2028)

- [x] **Phase 0:** System architecture design & hardware-software co-design (*Ocha Box* & *Dahila* specs).
- [ ] **Phase 1 (Current):** Python clinical data pipeline & **HL7 FHIR** schema validation.
- [ ] **Phase 2:** Local **Qwen-2.5 (3B)** integration for automated clinical quality scoring & FHIR JSON generation.
- [ ] **Phase 3:** **Rust** low-bandwidth gradient packer (`Zstd` compression + offline resilience queue).
- [ ] **Phase 4:** **FATE** standalone deployment & quality-weighted aggregation benchmark.
- [ ] **Phase 5:** Field pilot validation with *Docteur Solution* IoMT prototypes & v1.0 public release.

---

## 🤝 Contributing & Scientific Collaboration

We welcome contributions from AI researchers, Rust/Python engineers, biomedical engineers, and healthcare practitioners across Africa, China, and worldwide. 

* **Founder & Lead Architect:** [Votre Nom Complet]
* **Ecosystem:** Built in collaboration with the **Docteur Solution** digital health initiative.
* **License:** Distributed under the **Apache License 2.0**. See `LICENSE` for more information.

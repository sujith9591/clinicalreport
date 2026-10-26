# Clinical Decision Support Agent

**CP15 - Agentic AI Expert Capstone Project**

---

## 🎯 Project Status

✅ **FULLY OPERATIONAL** - All requirements met and verified  
📅 **Last Updated**: 2026-06-25  
🔗 **LLM**: Ollama llama3.2 @ 3.94.255.185:11434

---

## Quick Start

### Run the Agent
```bash
# Activate virtual environment
.venv\Scripts\activate

# Run with any patient ID
python main.py --patient_id PAT_001

# Check outputs
ls reports\sapk_*
```

### Expected Outputs
- `reports/sapk_{patient_id}_{timestamp}.json` - Structured report
- `reports/sapk_{patient_id}_{timestamp}.md` - Human-readable report
- `reports/sapk_{patient_id}_{timestamp}_citations.json` - Evidence citations
- `reports/guardrail_audit.csv` - Safety audit trail

---

## Key Features

✅ **Medical RAG** - Retrieves evidence from 13 clinical guidelines  
✅ **Safety Guardrails** - 4-layer validation (allergy, DDI, contraindication, dose)  
✅ **LLM Reasoning** - Evidence-based recommendations with citations  
✅ **Production-Ready** - Circuit breaker, retries, audit trail  
✅ **Agentic Behavior** - Multi-step reasoning, tool calling, self-correction

---

## Architecture

```
Patient Input → RAG Retrieval → LLM Reasoning → Guardrail Pipeline → Reports
                     ↓              ↓                   ↓              ↓
              (Guidelines)   (Differential Dx)   (Safety Checks)   (JSON/MD)
```

---

## Testing

### Run All Tests
```bash
# Connectivity test (run first)
python tools/test_ollama_connection.py

# Unit tests
python -m pytest tests/ -v

# Results: 7/7 tests passing ✅
```

---

## Documentation

### 📂 Core Documentation

| Document | Description |
|----------|-------------|
| [FINAL_STATUS.md](docs/capstone/FINAL_STATUS.md) | Complete project status |
| [SUCCESS_REPORT.md](docs/capstone/SUCCESS_REPORT.md) | Detailed success report |
| [E2E_TEST_RESULTS.md](docs/capstone/E2E_TEST_RESULTS.md) | End-to-end test results |

### 📂 Setup Guides

| Document | Description |
|----------|-------------|
| [QUICK_START.md](docs/setup/QUICK_START.md) | 5-minute setup guide |
| [BEST_PRACTICES.md](docs/setup/BEST_PRACTICES.md) | Production best practices |
| [PRODUCTION_SETUP.md](docs/setup/PRODUCTION_SETUP.md) | Full production guide |

### 📂 Capstone Documentation

| Document | Description |
|----------|-------------|
| [CAPSTONE_REQUIREMENTS_CHECKLIST.md](docs/capstone/CAPSTONE_REQUIREMENTS_CHECKLIST.md) | Requirements tracking |
| [DEMO_PREPARATION.md](docs/capstone/DEMO_PREPARATION.md) | Demo guide + PPT outline |
| [REQUIREMENTS_ALIGNMENT_SUMMARY.md](docs/capstone/REQUIREMENTS_ALIGNMENT_SUMMARY.md) | Requirements analysis |
| [CITATION_FIX_SUMMARY.md](docs/capstone/CITATION_FIX_SUMMARY.md) | Citation implementation |

### 📂 Testing Documentation

See [docs/testing/](docs/testing/) for comprehensive test results.

### 📂 Archived Documents

Old/redundant documentation moved to [docs/archive/](docs/archive/).

---

## Project Structure

```
Clinical_Decision_Support_Agent/
├── main.py                      # CLI entrypoint
├── config.yaml                  # Configuration
├── tools/                       # Test & utility scripts
│   ├── test_ollama_connection.py    # Connectivity test
│   └── test_prompt_size.py          # Prompt analyzer
├── requirements/                # Requirement documents
│   ├── CP15_...Requirements.docx    # Official requirements
│   ├── DAAI_CoP_Capstone...pdf      # Capstone presentation
│   └── pdf_page_*.txt               # Extracted pages
├── src/clinical_decision_support/
│   ├── agent.py                 # Main agent orchestration
│   ├── rag_engine.py            # RAG retrieval
│   ├── llm_client.py            # Ollama client
│   ├── guardrail_pipeline.py   # Safety validation
│   └── validators/              # 4 safety validators
├── tests/                       # Test suite (7/7 passing)
├── data/                        # Synthetic data
│   ├── patients.csv             # 50 patients
│   ├── drug_monographs.csv      # 30 drugs
│   ├── ddi_rules.csv            # 200+ interactions
│   └── clinical_guidelines/     # 13 guideline files
├── reports/                     # Generated outputs
└── docs/                        # Documentation (organized)
    ├── capstone/                # Capstone project docs
    ├── setup/                   # Setup guides
    ├── testing/                 # Test results
    └── archive/                 # Old docs
```

---

## Key Metrics

| Metric | Value |
|--------|-------|
| **Test Pass Rate** | 100% (7/7) |
| **Guardrail Accuracy** | 100% |
| **Citations Generated** | 5 per run |
| **Average Latency** | 75-80 seconds |
| **Confidence Score** | 0.8 (80%) |

---

## Requirements Compliance

✅ All CP15 requirements met (PDF page 8)  
✅ LLM endpoint configured (PDF page 11)  
✅ Synthetic data generated (PDF page 14)  
✅ Agentic behavior demonstrated  
✅ Production features implemented  
✅ Documentation complete  

**Status**: Ready for demo and PeopleRise assessment 🎯

---

## Support

For issues or questions:
1. Check [FINAL_STATUS.md](docs/capstone/FINAL_STATUS.md) for current status
2. Review [BEST_PRACTICES.md](docs/setup/BEST_PRACTICES.md) for troubleshooting
3. Run connectivity test: `python tools/test_ollama_connection.py`

---

**Disclaimer**: This output is for decision-support only and must be reviewed by a qualified clinician before any clinical action is taken.

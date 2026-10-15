# Breast Cancer Assistant (Heimdall)

An AI assistant that helps clinicians and patients reason about breast-cancer risk,
review mammography findings, and generate structured reports. It combines:

- A **clinical risk model** (scoring / tabular features).
- A **mammography deep-learning model** (with Grad-CAM explainability).
- An **LLM agent** that orchestrates tool calls under strict clinical safety rules.

> ⚠️ **Not a medical device.** Outputs are assistive and must be reviewed by a
> qualified clinician. See [`docs/limitations.md`](docs/limitations.md).

## Repository layout

```
.
├── contracts/          # Shared JSON contracts: clinical, mammo, validation, report
├── backend/app/        # FastAPI backend
│   ├── api/            # auth, chat, files, history endpoints
│   ├── schemas/        # Pydantic models
│   ├── services/       # auth, case, quota, token_budget, storage
│   ├── agent/          # agent loop, LLM client, memory, prompts
│   ├── tools/          # registry, validator, predictors, report builder
│   ├── rules/          # eligibility, red flags, risk factors (YAML)
│   ├── db/             # SQLAlchemy models, session, migrations
│   └── core/           # config, security, logging
├── model_service/      # Isolated inference service (clinical + mammography)
│   └── weights/        # Model weights — NOT committed to Git
├── frontend/           # Web client
├── training/           # Training configs, datasets, train/eval/export
├── tests/              # Unit & API tests
├── evaluation/         # Agent evals, load tests, reports
├── data/ & storage/    # Local data & uploads — NOT committed to Git
└── docs/               # Architecture, API contracts, limitations, results
```

## Getting started

1. **Copy env template** and fill in secrets:
   ```bash
   cp .env.example .env
   ```
2. **Backend:**
   ```bash
   cd backend
   pip install -r requirements.txt   # (to be added)
   uvicorn app.main:app --reload
   ```
3. **Model service:**
   ```bash
   cd model_service
   pip install -r requirements.txt   # (to be added)
   uvicorn main:app --port 8001
   ```
4. **Frontend:** see [`frontend/README.md`](frontend/README.md).

## Documentation

- [Architecture](docs/architecture.md)
- [API contracts](docs/api_contracts.md)
- [Limitations & disclaimers](docs/limitations.md)
- [Evaluation results](docs/evaluation_results.md)

## License

See [LICENSE](LICENSE).

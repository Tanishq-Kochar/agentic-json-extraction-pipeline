# Agentic Self-Correcting JSON Extraction Pipeline

A backend data pipeline that leverages open-source LLMs to parse chaotic, unstructured IT incident logs into strict, database-ready JSON schemas. 

Instead of trusting the LLM blindly, this system utilizes an autonomous agentic loop: it intercepts malformed outputs via Pydantic validation, generates programmatic error tracebacks, and forces the model to self-correct its formatting in real-time.

## System Architecture

1. **Data Ingestion:** Streams real-world, unstructured developer incident reports directly from the `lewtun/github-issues` Hugging Face dataset.
2. **High-Speed Inference:** Utilizes Groq's API engine running `Llama-3.1-8b-instant` for ultra-fast, low-latency text processing.
3. **Deterministic Gateway:** Enforces output structure using Pydantic `BaseModel` classes, ensuring extracted data meets strict type and formatting constraints (e.g., forcing uppercase severity flags).
4. **Agentic Correction Loop:** If the LLM hallucinates a schema key or violates a data type, the pipeline catches the `ValidationError`, injects the exact traceback back into the prompt context, and executes a retry loop until the data is pristine.
5. **Telemetry Dashboard:** Processes batches of incident logs and outputs a performance matrix tracking execution time, success rates, and retry counts.

## Getting Started

### Dependencies
```bash
pip install pydantic groq datasets

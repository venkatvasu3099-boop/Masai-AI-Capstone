# Part 4: Intelligent System with Production Guardrails - Water Quality

## Project Overview
This folder contains the final Part 4 submission for the Applied AI & ML Essentials Capstone Project. This module wraps our LLM-powered water quality evaluation engine within strict production-ready input and output guardrails. This architecture guarantees system stability, prevents malicious user exploitation, and eliminates data validation runtime crashes.

## Dependencies
This module runs entirely using standard Python infrastructure along with network utilities:
* requests
* google-colab (if deploying via Google Colab environment)

## Guardrail Architecture & Design Decisions
To transform a basic LLM integration into a reliable production-conscious system, we implemented two operational guardrail layers:

### 1. Input Guardrails (Pre-Processing Layer)
Before any request is transmitted to the external OpenRouter API gateway, the input data undergoes a local evaluation step:
* **Scientific Boundary Checking:** Validates that metrics fall into logically sound parameters (e.g., verifying that a pH value sits correctly between 0 and 14, and ensuring chemical PPM volumes are not negative values).
* **Prompt Injection Defense:** Scans the incoming contextual notes for malicious adversarial phrases (such as *"ignore previous instructions"* or *"system prompt"*). If an anomaly is identified, the application safely rejects the processing request before interacting with the LLM API, preserving server context safety.

### 2. Output & Fallback Guardrails (Post-Processing Layer)
Generative models occasionally introduce unexpected formatting drift or token corruptions. Our downstream pipeline protects against this using:
* **Structural Schema Verification:** Validates that the returned output from the LLM contains all required production telemetry keys (`ph_evaluation`, `chemical_balance`, `safety_status`, and `recommended_treatment`).
* **Graceful Exception Fallbacks:** If the API encounters network timeout disconnects, or if the model outputs a malformed string that cannot be loaded by `json.loads()`, the system intercepts the error. Instead of passing an exception back to the interface, it injects a highly structured, predetermined safe fallback JSON error payload.

## Setup and Execution Instructions
1. Open the file `part4_guardrails.ipynb` in your notebook environment.
2. Confirm your environment variable credentials are properly injected into your active workspace.
3. Run the script cells to see the input verification blocks catch error parameters and malicious phrases gracefully.

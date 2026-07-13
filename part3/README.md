# Part 3: LLM Integration with Structured Outputs - Water Quality Analysis

## Project Overview
This folder contains the Part 3 submission for the Applied AI & ML Essentials Capstone Project. The objective of this phase is to integrate a Large Language Model (LLM) via a public API to perform intelligent analysis on water quality metrics. The system enforces structured outputs, ensuring the model returns parsed, programmatic JSON data rather than unstructured natural language text.

## Dependencies
To execute this script, you will need Python along with the following standard packages:
* requests
* google-colab (if running within Google Colab environment)

You can install the standard network dependency via your terminal:
`pip install requests`

## Environment Variables & Security
As mandated by production guidelines, no API keys are hardcoded into the source code. The code securely interfaces with OpenRouter via the local environment.
* The system looks for an environment variable named: `OPENROUTER_API_KEY`
* Ensure your root `.env` file contains this key locally, or add it to your Google Colab "Secrets" (🔑 icon) panel with the name `OPENROUTER_API_KEY` before running.

## Setup and Execution Instructions
1. Open the script or notebook `part3_llm.ipynb` in your environment.
2. Ensure your OpenRouter API key is loaded into your workspace environment or Secrets panel.
3. Run the notebook. The script executes an API call using a standard HTTP POST request with a JSON payload and processes the output.

## System Integration & Design Decisions
* **API Provider:** OpenRouter was chosen as the API gateway because it handles standardized HTTP POST requests with a JSON body and returns clean JSON responses.
* **Model Selection:** The system utilizes `openai/gpt-oss-120b:free` (or an active equivalent free model), providing robust natural language reasoning capabilities on an open ecosystem tier.
* **Structured Output Enforcements:** To ensure the system delivers reliable, schema-bound downstream data, the system relies on strict prompt engineering frameworks. The prompt forces the LLM to output a raw JSON structure matching four key operational keys: `ph_evaluation`, `chemical_balance`, `safety_status`, and `recommended_treatment`.
* **Data Defense & Resiliency:** A programmatic cleaning block intercepts the LLM output to strip away accidental markdown identifiers (such as ` ```json ` tags) before feeding the string into the native Python `json.loads()` parser. This ensures the output can be directly integrated into production code rules without throwing data-type exceptions.

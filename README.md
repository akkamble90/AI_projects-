# AI Legacy Code Summarizer

A Generative AI tool designed to analyze, explain, and document complex legacy code (COBOL, Java, C++, Python) into simple English business logic. It leverages **AWS Bedrock** and **Anthropic Claude 3.5 Sonnet** with a self-correcting validation pipeline to ensure accuracy.

## Key Features

* **Logic Extraction**: Converts raw, complex code into clear, non-technical business logic summaries.
* **Self-Correcting Pipeline**: Implements a two-step AI chain (Draft → Validate) where the model critiques its own work to reduce hallucinations and catch edge cases.
* **Cross-Region Resilience**: Automatically routes requests to optimal AWS regions (e.g., EU-Central-1) using **Inference Profiles** to bypass regional model availability restrictions.
* **Secure Tunneling**: Deploys a private local server to the public web using secure tunneling, allowing for easy sharing and remote access.

## Architectural Orchestration

The application follows a **Chain-of-Thought (CoT)** architecture orchestrated by **LangChain**:

1.  **Input Layer**: The user submits a legacy code snippet via the **Streamlit** frontend.
2.  **Orchestration Layer (LangChain)**:
    * **Prompt A (Drafting)**: The system injects the code into a "Developer Persona" prompt to generate an initial explanation.
    * **Prompt B (Validation)**: The output of Prompt A is fed back into the LLM with a "QA Persona" prompt to verify accuracy against the original code.
3.  **Inference Layer (AWS Bedrock)**:
    * The request is routed to **Claude 3.5 Sonnet** via AWS Inference Profiles (`eu.anthropic.claude...`), ensuring high availability and compliance with data residency.
4.  **Presentation Layer**: The validated summary is parsed and rendered back to the user interface.

##  Technical Aspects

* **Model**: Anthropic Claude 3.5 Sonnet (via AWS Bedrock)
* **Framework**: LangChain (Python)
* **Infrastructure**: Serverless Inference on AWS
* **Frontend**: Streamlit (Reactive Web UI)
* **Deployment**: Ngrok Tunneling for public accessibility from private runtime environments (like Google Colab).

#  AI Legacy Code Summarizer

A Generative AI tool designed to analyze, explain, and document complex legacy code (COBOL, Java, C++, Python) into simple English business logic. It leverages **AWS Bedrock** and the advanced **Anthropic Claude Sonnet 4** model with a self-correcting validation pipeline to ensure accuracy.

##  Key Features

* **Logic Extraction**: Converts raw, complex code into clear, non-technical business logic summaries using the latest Sonnet 4 reasoning engine.
* **Self-Correcting Pipeline**: Implements a two-step AI chain (Draft → Validate) where the model critiques its own work to reduce hallucinations and catch edge cases.
* **Cross-Region Resilience**: Automatically routes requests to optimal AWS regions (EU-Central-1) using **Inference Profiles** to bypass regional availability restrictions.
* **Secure Tunneling**: Deploys a private local server to the public web using secure tunneling, allowing for easy sharing and remote access.

## Architectural Orchestration

The application follows a **Chain-of-Thought (CoT)** architecture orchestrated by **LangChain**:

1.  **Input Layer**: The user submits a legacy code snippet via the **Streamlit** frontend.
2.  **Orchestration Layer (LangChain)**:
    * **Prompt A (Drafting)**: The system injects the code into a "Developer Persona" prompt to generate an initial explanation.
    * **Prompt B (Validation)**: The output of Prompt A is fed back into the LLM with a "QA Persona" prompt to verify accuracy against the original code.
3.  **Inference Layer (AWS Bedrock)**:
    * The request is routed to **Anthropic Claude Sonnet 4** (`anthropic.claude-sonnet-4-20250514-v1:0`) via AWS Inference Profiles, ensuring high availability and compliance with data residency.
4.  **Presentation Layer**: The validated summary is parsed and rendered back to the user interface.

##  Technical Aspects

* **Model**: Anthropic Claude Sonnet 4 (via AWS Bedrock)
* **Framework**: LangChain (Python)
* **Infrastructure**: Serverless Inference on AWS
* **Frontend**: Streamlit (Reactive Web UI)
* **Deployment**: Ngrok Tunneling for public accessibility from private runtime environments (like Google Colab).

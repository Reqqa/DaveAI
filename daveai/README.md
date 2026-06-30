# DaveAI 

> An Autonomous Event-Driven Workflow AI Agent for Strategic People Operations.

DaveAI is an intelligent internal team member built to streamline employee lifecycle tracking, automate peer/incident recognition, and provide personalized growth pathways. Built on top of an event-driven retrieval-augmented generation (RAG) architecture, DaveAI connects daily engineering realities directly to People Ops actions.

## Key Capabilities

*   **Continuous Employee Development:** Analyzes unstructured work logs and post-mortems to deliver real-time micro-learning modules and log skill progression tracking.
*   **Dynamic Journey Mapping:** Monitors critical timeline milestones (e.g., the 18-month tenure mark) and team macro-trends to provide managers with proactive retention playbooks.
*   **Algorithmic Employee Recognition:** Evaluates team telemetry against the corporate culture handbook to instantly identify core-value alignment and draft spot-bonus allocations.

##  System Architecture & Tech Stack

DaveAI orchestrates data flows across your entire engineering and operational ecosystem using a production-grade suite of integrations:

*   **Agentic Orchestration:** Built as a **Workflow AI Agent** utilizing platform-native Large Language Models (LLMs) to reason, synthesize text context, and generate structured actions.
*   **Ingestion Pipeline:** Connected via **GitHub Webhooks (REST APIs)** to actively listen for incoming technical documentation, pull requests, and incident post-mortems.
*   **Cognitive Storage Engine:** Utilizes **Supabase (PostgreSQL with `pgvector`)** to perform parallel hybrid searches (dense vector embeddings + BM25 lexical keywords) while strictly filtering data permissions by `Employee` and `Role`.
*   **Dynamic AI Policy Enforcement:** Houses programmatic verification checks (e.g., checking the rewards ledger to enforce a 90-day spot-bonus cooling-off period) before taking financial action.
*   **Human-in-the-Loop Escalation:** Automatically routes compliance violations or complex operational edge cases directly to the human-supervised **Autos Workbench** for structural manual review.
*   **Multi-Channel Execution:** Fires processed natural language actions concurrently out to **Slack Webhooks** (for public community `#kudos` feeds) and the **Microsoft Graph API** (to inject retention agendas directly into managers' Outlook 1-on-1 invites).

## 💻 Getting Started

### Prerequisites
* A Supervity Workspace with access to the **Workflow AI Agent** workspace.
* A Supabase project initialized with `pgvector` enabled.
* Administrative webhooks configuration access on your GitHub repository.
* API keys and app credentials for Slack and Microsoft 365.

### Environment Setup
Configure the following secure environment variables within your agent's workflow variables panel:
```env
SUPABASE_URL=your_supabase_project_url
SUPABASE_SERVICE_ROLE_KEY=your_secure_db_key
GITHUB_WEBHOOK_SECRET=your_repository_webhook_secret
SLACK_WEBHOOK_URL=your_target_kudos_channel_webhook
MICROSOFT_GRAPH_CLIENT_SECRET=your_m365_app_secret

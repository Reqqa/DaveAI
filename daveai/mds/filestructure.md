daveai-peopleops/
├── .github/
│   └── workflows/              # CI/CD pipelines for building the Rust binary
├── config/
│   ├── supervity_workflow.json # Exported Supervity DaveAI workflow template setup
│   └── dynamic_policy.json     # Declarative policy thresholds (cooldown configurations)
├── db/
│   ├── migrations/             # SQL database migration tracking
│   │   ├── 01_init_schema.sql  # Employee relational tables
│   │   └── 02_add_pgvector.sql # pgvector setups and embedding vector columns
│   └── seeds/
│       └── culture_handbook.sql# Pre-calculated handbook embedding data
├── src/
│   ├── core/
│   │   ├── mod.rs
│   │   ├── embeddings.rs       # Interface structures for embedding logic
│   │   └── policy_engine.rs    # Verification logic (90-day cooldown evaluation)
│   ├── integrations/
│   │   ├── mod.rs
│   │   ├── github.rs           # Parsing payload structures from GitHub webhooks
│   │   ├── slack.rs            # Generating typed Slack Block Kit JSON schemas
│   │   └── supabase.rs         # Database pool & hybrid pgvector queries (via sqlx)
│   ├── main.rs                 # Web server entry point (Axum / Actix-web listener)
│   └── errors.rs               # Custom type safe error handling matching Autos Workbench
├── Cargo.toml                  # Project manifest, compilation targets, and dependencies
├── .env.example                # Template for database URLs and API authorization tokens
└── README.md                   # Technical onboarding documentation

[1. ENGINEERING ACTION]  ─►  [2. INGESTION BRIDGE]  ─►  [3. SECURITY & POLICY]
 Engineer merges a PR         GitHub Webhook captures    Rust microservice checks
 or files a Post-Mortem.      & forwards JSON payload.   Supabase for 90-day cooldown.
                                                                  │
                                      ┌───────────────────────────┴───────────────────────────┐
                                      ▼ [Passed]                                              ▼ [Violated]
                           [4A. COGNITIVE PROCESSING]                              [4B. HUMAN ESCALATION]
                            Supervity Workflow executes                             Workflow halts automation.
                            RAG query on pgvector rules.                            Pushes payload details to
                                      │                                             Autos Workbench UI.
                                      ▼                                                       │
                           [5. CONTEXT SYNTHESIS]                                             │
                            DaveAI LLM analyzes context                                       │
                            & builds custom output strings.                                   │
                                      │                                                       │
                                      ▼                                                       ▼
                           [6. MULTI-CHANNEL OUTPUT]                                [7. MANUAL OVERRIDE]
                            • Public Slack #kudos card.                             HR Manager reviews ticket.
                            • Private Slack DM to Manager.                          Approves or downgrades path
                            • Profile metrics updated in DB.                        to resume execution.


## User Flow 
# AI-Powered Engineering Recognition Workflow
## Step 1: Organic Trigger (Engineering Team)
### User Action
Tanni (an L2 Engineer) completes a large-scale database migration recovery at **2:00 AM** and merges a standard Markdown document into the company's enterprise GitHub repository:
```text
/incident-logs/postmortem-db-04.md
```
### System Event
Once the pull request is merged, GitHub automatically generates a **Webhook** containing:
- Raw Markdown file contents
- Committer metadata (`employee_id`)
- Repository information
- Commit metadata
---
## Step 2: Ingestion Gateway (Rust Microservice)
### System Event
A high-performance **Rust Axum** web server receives the incoming GitHub webhook via an HTTP `POST` request.
### Processing
Using **Serde**, the JSON payload is deserialized into strongly typed Rust structures.
The service performs:
- Markdown cleanup and normalization
- Raw incident text extraction
- Employee metadata extraction
- Repository parameter parsing
- Payload validation
The cleaned event is now ready for downstream processing.
---
## Step 3: Compliance Validation Check (Guardrail Engine)
### System Event
The Rust service asynchronously queries the **Supabase Rewards Ledger** using **sqlx**.
### Decision Logic
#### Path A — Compliance Passed ✅
If **no financial reward** has been issued to Tanni within the previous **90 days**:
- Compliance passes
- The workflow creates:
```json
{
  "cooldown_passed": true
}
```
- The payload is forwarded to the **Supervity Workflow Agent REST API**
---
#### Path B — Policy Violation ⚠️
If a previous reward exists (for example, **45 days ago**):
- Compliance fails
- The workflow creates:
```json
{
  "cooldown_passed": false
}
```
- The request bypasses the recognition workflow
- Execution is routed directly into the HR escalation path
---
## Step 4: Cognitive Retrieval & Synthesis (Supervity Workflow + LLM)
### System Event
When **Path A** is selected, the Supervity Workflow Agent performs AI-powered reasoning.
### Retrieval Phase
The workflow searches the **Supabase pgvector knowledge base** using a **Hybrid Search** approach:
- Dense Vector Search
- BM25 Lexical Search
Example concepts retrieved include:
- Crisis mentorship
- Operational excellence
- Customer ownership
- Incident response leadership
- Collaboration
### LLM Processing
The retrieved corporate values and Tanni's incident log are supplied to the **DaveAI Native LLM**.
The model transforms engineering-specific language into professional business communication.
### Generated Outputs
The LLM produces:
- Public recognition message
- Private manager coaching brief
- Employee skill profile updates
---
## Step 5: Interactive Delivery (Slack Workspace)
### System Event
DaveAI simultaneously triggers multiple outbound integrations.
### Public Recognition
A rich **Slack Block Kit** message is posted to:
```text
#eng-wins
```
The announcement highlights:
- Tanni's late-night recovery effort
- Engineering impact
- Alignment with company values
---
### Manager Coaching
A private Slack Direct Message is sent to Tanni's manager.
Example:
> Hi Sarah,
>
> Tanni's 18-month tenure milestone is next week.
>
> Based on her database migration recovery, here are recommended discussion points for tomorrow's 1-on-1 meeting...
---
### Employee Profile Update
The workflow performs a transactional update inside Supabase.
Example:
```
crisis_mentorship_score += 1
```
The employee's long-term growth profile is updated automatically.
---
## Step 6: Human-in-the-Loop Management (Autos Workbench)
### Trigger Condition
This stage executes **only if Path B occurs**.
### System Behavior
The automated workflow stops immediately.
No Slack messages are delivered.
No recognition is published.
### HR Review
The HR Director opens the **Autos Workbench Dashboard** and sees a pending approval ticket:
```text
REWARD POLICY EXCEPTION:
Cooldown Conflict for Employee Tanni
```
The dashboard displays:
- Original incident post-mortem
- Historical reward records
- Cooldown policy explanation
- AI-generated recommendation
### Available Actions
#### Approve Exception
**Action**
Continue the workflow despite the cooldown violation.
**Result**
- Recognition workflow resumes
- Slack kudos card is published
- Standard recognition pipeline continues
---
#### Downgrade to Non-Monetary Recognition
**Action**
Modify the LLM prompt to remove financial reward eligibility.
**Result**
The workflow generates:
- Team recognition
- Public appreciation
- Manager coaching
No monetary bonus or financial reward is issued.
---

# Overall Workflow

```text
GitHub Merge
      │
      ▼
Rust Axum Webhook Receiver
      │
      ▼
Serde Payload Processing
      │
      ▼
Supabase Reward Cooldown Check
      │
      ├───────────────┐
      │               │
      ▼               ▼
 Path A           Path B
 Passed           Violated
      │               │
      ▼               ▼
Supervity       Autos Workbench
Workflow        HR Approval
      │               │
      ▼               │
DaveAI LLM            │
      │               │
      ▼               │
Slack + Supabase ◄────┘
```

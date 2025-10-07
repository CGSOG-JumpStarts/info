# **Comprehensive Guide to Defining Non-Ambiguous Deliverables in Generative AI Projects**
## **Best Practices for Writing Unambiguous SOWs with the S.M.A.R.T.A.I. Method**

---

## **Executive Summary**

### **The Strategic Imperative for Clarity**

Generative AI projects are fundamentally different from traditional software development. They are inherently probabilistic, dependent on data quality, and often exploratory in nature. Ambiguous statements in Statements of Work (SOWs) such as "build RAG with 95% accuracy," "create chatbot with 2 personas," or "develop 3 agentic use cases" are not just imprecise—they are a direct path to:

- **Project overruns** (30-50% timeline extensions due to scope clarification)
- **Client disputes** over whether deliverables are "complete"
- **Engineering waste** building features not actually required
- **Delayed revenue recognition** due to acceptance criteria disputes
- **Damaged client relationships** and reduced repeat business

### **The Business Case for Precision**

**Without Clear Deliverables:**
- Scope creep becomes unmanageable
- Acceptance testing becomes subjective and contentious
- Teams lose morale due to shifting goalposts
- Client satisfaction scores decline
- Project profitability erodes

**With Clear Deliverables:**
- ✅ Reduced change orders and predictable project scoping
- ✅ Faster client sign-off and project closure
- ✅ Improved team efficiency and morale
- ✅ Higher client satisfaction and reference-ability
- ✅ Defensible metrics that demonstrate value

### **Purpose of This Document**

This guide establishes **clear standards** for defining, scoping, and validating generative AI deliverables so that every AI engagement has:
- Measurable outcomes
- Defensible metrics
- Repeatable quality
- Mutually understood success criteria
- Transparent evaluation processes

It is designed to equip **sales, solutioning, and delivery teams** with a shared language to define success, manage client expectations, and ensure profitable, successful engagements.

---

## **Table of Contents**

1. Core Principles & Frameworks
2. Common Pitfalls & How to Avoid Them
3. Deliverable Taxonomy
4. The S.M.A.R.T.A.I. Framework
5. Detailed Specification Templates
6. Metrics & Acceptance Criteria Catalog
7. Evaluation Framework
8. From Vague to Verifiable: Rewrite Examples
9. SOW Structure & Required Appendices
10. Governance & Review Process
11. Implementation Guide
12. Quick Reference Materials

---

## **1. Core Principles & Frameworks**

### **1.1 Fundamental Principles**

#### **Principle 1: Define Everything, Assume Nothing**
Every technical term, metric, and concept must be explicitly defined in the SOW. What seems obvious to an AI engineer may be completely unclear to a client stakeholder.

#### **Principle 2: The "Stranger Test"**
Could a stranger with technical knowledge understand exactly what you're committing to deliver? If not, it's too ambiguous.

#### **Principle 3: Measurable Outcomes Over Features**
Never sell a feature; sell a **verified outcome** with a named metric, dataset, and acceptance test. Shift from listing capabilities to defining observable, quantifiable results.

#### **Principle 4: Scope the Asset, Not the Aspiration**
Deliver a named artifact or capability with a stable interface, not a vague promise of improvement.

#### **Principle 5: Observable & Testable**
Every statement must be testable in a CI-like evaluation harness. If you can't measure it objectively, you can't deliver it reliably.

#### **Principle 6: Version Everything**
Data (EvalSet vX.Y), model (Provider+Model+Params), code, prompts, tools, environments—all must be versioned and tracked.

#### **Principle 7: Define Acceptance Once**
One acceptance run with fixed seeds/parameters; store results and report. No moving targets.

#### **Principle 8: Quantify Everything Possible**
Replace qualitative terms with specific numbers, percentages, or measurable behaviors.

#### **Principle 9: State What's Excluded**
Ambiguity often hides in what's NOT said. Explicitly state scope boundaries and out-of-scope items.

#### **Principle 10: Co-create Definitions with the Client**
Use definition workshops as part of the sales process to ensure alignment and build trust. The SOW should document a shared understanding, not impose your own.

### **1.2 Guiding Philosophy**

> **Good AI SOWs don't promise features. They promise measurable outcomes, observable systems, and auditable performance.**

The goal is not perfection but **precision in process**. AI performance is iterative, so define the *process and metrics* for evaluation and improvement, not just a static, final number.

---

## **2. Common Pitfalls & How to Avoid Them**

### **2.1 Universal Pitfalls**

| Pitfall | Description | Impact | Solution |
|---------|-------------|--------|----------|
| **Undefined Metrics** | Accuracy, precision, or recall mentioned without defining data, test set, or measurement method | Disputes over whether targets are met | Use Metrics Catalog (Section 6) |
| **Unclear Use Case Boundaries** | Scope defined by quantity, not outcome | Feature creep and scope disputes | Use Use Case Template (Section 5.3) |
| **Feature-Driven Instead of Value-Driven** | Focus on technical capability vs. business impact | Deliverables that don't solve the actual problem | Tie every deliverable to business metric |
| **Lack of Validation Framework** | No acceptance criteria for quality or observability | Projects "done" but not usable | Define evaluation plan upfront (Section 7) |
| **Vague Terminology** | Terms like "intelligent," "robust," "high quality" | Subjective acceptance criteria | Use glossary and specific definitions |
| **The Demo Trap** | Client sees impressive demo, assumes production will match | Unrealistic expectations | Explicitly state demo conditions vs. production |
| **Accuracy Theater** | Claims like "95% accuracy" without context | Meaningless performance claims | Always specify: metric + dataset + baseline |
| **Subjective Acceptance** | "Client must be satisfied with quality" | Unresolvable disputes | Replace with objective, testable criteria |
| **Implied Capabilities** | Client assumes features from consumer AI tools | Scope gaps and disappointment | Explicitly state what system CANNOT do |

### **2.2 Category-Specific Pitfalls**

#### **RAG Systems**
- ❌ "95% accuracy" → What is being measured?
- ❌ "Custom RAG" → What makes it custom?
- ✅ Solution: Use RAG Specification Template (Section 5.1)

#### **Conversational AI**
- ❌ "Chatbot with 2 personas" → What defines a persona?
- ❌ "Natural conversations" → What makes it natural?
- ✅ Solution: Use Persona Specification Card (Section 5.2)

#### **Agentic Workflows**
- ❌ "3 agentic use cases" → What constitutes a use case?
- ❌ "Intelligent automation" → What behaviors are intelligent?
- ✅ Solution: Use Agentic Use Case Specification (Section 5.3)

#### **Content Generation**
- ❌ "High-quality content" → Measured how?
- ❌ "Brand-appropriate" → Based on what criteria?
- ✅ Solution: Use Content Generation Specification (Section 5.4)

---

## **3. Deliverable Taxonomy**

### **3.1 Capability Deliverables**
These are functional systems or components:
- **Retrieval-Augmented QA (RAG)** - Question answering with source grounding
- **Conversational Assistant** - Multi-turn dialogue systems
- **Agentic Workflow/Orchestration** - Autonomous task completion
- **Classifier/Router** - Intent detection and routing
- **Summarizer** - Content condensation
- **Extractor** - Structured data extraction
- **Fine-tuned Model** - Custom-trained models
- **Evaluation Harness** - Testing and benchmarking systems
- **Safety Layer** - Content moderation and guardrails
- **Observability Stack** - Monitoring and logging

### **3.2 Asset Deliverables**
These are artifacts and resources:
- **Datasets** - EvalSet, GoldenSet, training data
- **Prompt Library** - Versioned prompts and templates
- **Tool Catalog** - Available functions and APIs
- **Data Pipelines** - Ingestion and processing workflows
- **Knowledge Index** - Searchable document repositories
- **Dashboards** - Metrics visualization
- **Playbooks** - Operational procedures
- **Runbooks** - Incident response guides
- **Architecture Docs** - System design documentation

### **3.3 Stage Deliverables**
These define maturity levels:
- **PoC (Proof of Concept)** - Lab environment, demonstration
- **Pilot** - Limited production, controlled user group
- **Production** - Full deployment with SLA/SLO, on-call support
- **Handover** - Complete documentation, training, transition

---

## **4. The S.M.A.R.T.A.I. Framework**

Every deliverable should meet the **S.M.A.R.T.A.I.** criteria—a GenAI adaptation of SMART goals:

| Attribute | Description | Questions to Answer | Example |
|-----------|-------------|---------------------|---------|
| **S - Specific** | Define precisely what will be built and what it will do | - What exact capability? <br>- What components? <br>- What interfaces/formats? | "RAG chatbot for internal policy documents with conversational retrieval over 10k PDFs" |
| **M - Measurable** | Quantify performance through defined metrics and evaluation sets | - What metrics define success? <br>- What are the numerical thresholds? <br>- How will measurement be performed? | "≥85% factual accuracy on 500 QA pairs measured via RAGAS Factuality" |
| **A - Achievable** | Ensure deliverables fit time, data, and budget constraints | - Is this technically feasible? <br>- Are resources available? <br>- Are timelines realistic? | "Fine-tuning 10k samples using Azure OpenAI GPT-4-Turbo within 8-week delivery" |
| **R - Relevant** | Tie outcomes to measurable business impact | - Does this solve the actual problem? <br>- Will it integrate with existing systems? <br>- What's the business value? | "Reduces manual RFP response drafting time by 40%" |
| **T - Time-Bound** | Set delivery windows and validation checkpoints | - What is the delivery date? <br>- What are intermediate milestones? <br>- When is acceptance testing? | "Phase 1: prototype in 3 weeks; Phase 2: production in 6 weeks" |
| **A - Auditable** | Deliverables must include test data, evaluation reports, and traceability logs | - Can results be reproduced? <br>- Are all runs logged? <br>- Is there a clear audit trail? | "All runs logged in Langfuse; eval results stored in Azure Blob and shared via dashboard" |
| **I - Interpretable** | Model outputs must be explainable with traceability and confidence scoring | - Can we explain decisions? <br>- Are sources traceable? <br>- Is confidence indicated? | "RAG includes citation links and confidence scores per response" |

### **4.1 Alternative Framework: S.M.A.R.T.-T**

For teams preferring the traditional SMART with an additional T:

- **S** - Specific
- **M** - Measurable  
- **A** - Achievable
- **R** - Relevant
- **T** - Time-bound
- **+T** - **Testable** (How will we verify success?)

Both frameworks work; choose one and use it consistently across all SOWs.

---

## **5. Detailed Specification Templates**

### **5.1 RAG System Specification Template**

Use this template for any Retrieval-Augmented Generation project:

```markdown
## Deliverable: [RAG System Name]

### Objective
[What business problem does this solve?]
Example: "To allow customer support agents to quickly find answers to technical 
questions from our internal knowledge base."

### Data Sources (Frozen)
[Exhaustive list of all corpora to be indexed]
- SharePoint Site: [Specific site name/URL]
- Confluence Space: [Space key]
- Public Documentation: [Specific URLs]
- Internal Wikis: [Specific paths]
- [Add all sources with exact identifiers]

**Exclusions:** [What data is NOT included]

### Indexing Strategy

**Chunking Strategy:**
- Method: [e.g., "Recursive character splitting"]
- Chunk Size: [e.g., "1000 characters"]
- Overlap: [e.g., "200 characters"]

**Metadata Extraction:**
- Fields stored: [e.g., `source_url`, `document_title`, `last_modified_date`, 
  `document_type`, `department`]

**Freshness Policy:**
- Update Cadence: [e.g., "Daily incremental, weekly full rebuild"]
- Date Filters: [e.g., "Only documents with `RFPDueDate` ≤ query date"]
- Violation Rate Target: [e.g., "= 0%"]

### Retrieval Strategy
- Method: [e.g., "Hybrid search combining vector similarity (text-embedding-ada-002) 
  with keyword-based BM25"]
- Top-K Retrieved: [e.g., "8 chunks"]
- Reranking: [If applicable, describe method]

### Generation Model
- Model: [e.g., "OpenAI GPT-4o" or "Anthropic Claude 3.5 Sonnet"]
- Temperature: [e.g., "0.2"]
- Top_p: [e.g., "1.0"]
- Max Tokens: [e.g., "1000"]

### Evaluation Dataset
[Define the "golden dataset" for testing]
- Name: [e.g., "EvalSet v1.2"]
- Size: [e.g., "500 question-answer pairs"]
- Source: [e.g., "Client SME-validated, stratified by domain"]
- Sampling: [e.g., "Representative of production query distribution"]
- Storage: [Location and access method]

### Acceptance Criteria

**Retrieval Metrics:**
- **Recall@8**: ≥ 0.85
  - Definition: "For 85% of test questions, at least one relevant document 
    appears in the top 8 retrieved chunks"
- **MRR (Mean Reciprocal Rank)**: ≥ 0.60
  - Definition: "Average reciprocal rank of first relevant document"
- **Coverage**: ≥ 0.95
  - Definition: "95% of queries return at least one relevant document"

**Answer Quality Metrics:**
- **Faithfulness/Groundedness**: ≥ 0.90
  - Method: "RAGAS Faithfulness score or calibrated LLM-judge rubric"
  - Validation: "Validated on 100-sample human-labeled subset with IAA κ ≥ 0.7"
- **Relevance**: ≥ 0.80
  - Method: "Rubric level ≥4/5 by calibrated LLM-judge"
- **Source Attribution Rate**: ≥ 0.90
  - Definition: "90% of answers include at least one correct source citation"
- **Hallucination Rate**: < 5%
  - Definition: "Claims not supported by retrieved context"

**Performance Metrics:**
- **P95 Latency**: ≤ 2.5 seconds
- **P50 Latency**: ≤ 1.5 seconds
- **Cost per Query**: ≤ $0.02 (at 95th percentile)
- **Throughput**: [e.g., "Supports 10 concurrent queries"]

**Quality Gates:**
- PII Redaction: [If applicable, define pipeline]
- Citation Coverage: ≥ 90%
- Confidence Scoring: [Define if included]

### Acceptance Run
- **Single Frozen Run:** Results from one evaluation using fixed parameters
- **Logging:** All runs logged in [Observability tool, e.g., "Langfuse"]
- **Report:** Acceptance report attached to deliverable documentation

### Observability
- Platform: [e.g., "Langfuse", "Azure AI Foundry", "Datadog"]
- Logged Metrics: [Query, Retrieved Docs, Generated Answer, Latency, Cost]
- Dashboard: [Link or description]
- Alerts: [Define alert thresholds]

### Security & Compliance
- Data Residency: [e.g., "US East"]
- Encryption: [In transit and at rest specifications]
- Access Controls: [RBAC definitions]
- Privacy: [PII handling procedures]

### Artifacts Delivered
- [ ] Ingestion scripts and pipeline code
- [ ] Evaluation dataset (EvalSet v1.2)
- [ ] Acceptance test report with metrics
- [ ] Metrics dashboard (live link)
- [ ] Architecture diagram
- [ ] Prompt library (versioned)
- [ ] User/Admin documentation
- [ ] Runbook for operations

### Explicitly Out of Scope
- Multi-turn conversational memory
- Questions requiring synthesis across >5 documents
- Real-time document updates (batch only)
- Languages other than English
- [Add other exclusions]

### Timeline
- Milestone 1: [Component] by [Date]
- Milestone 2: [Component] by [Date]
- Final Delivery: [Date]
- Acceptance Testing: [Date range]

### Sign-off
- Owner: [Name, Title]
- Approval Date: [Date]
```

---

### **5.2 Persona Specification Card Template**

Use this for any conversational AI or chatbot project involving multiple personas:

```markdown
## Persona Specification: [Persona Name]

### Persona Identity
- **Name/ID**: [e.g., "SupportBot_v1", "Persona_Technical"]
- **Version**: [e.g., "1.0"]
- **Last Updated**: [Date]

### Role & Purpose
[Single, clear sentence defining primary function]
Example: "A friendly and professional first-line support agent for product FAQs."

### Knowledge Domain (Exact Boundaries)
[Define explicit boundaries of expertise]

**Data Sources:**
- SharePoint: [Specific sites]
- Confluence: [Specific spaces]
- Web Pages: [Specific URLs]
- Documents: [Specific file lists]

**Topics Covered:**
- [Topic 1]
- [Topic 2]
- [Topic 3]

**Topics NOT Covered:**
- [Excluded topic 1]
- [Excluded topic 2]

### Tone of Voice
[Adjectives describing communication style]
- [e.g., "Professional"]
- [e.g., "Patient"]
- [e.g., "Concise"]
- [e.g., "Empathetic"]
- [e.g., "Clear"]

### Personality Traits & Behaviors
[Specific, observable behaviors]
- [e.g., "Always introduces itself at start of conversation"]
- [e.g., "Uses 'we' instead of 'I' when referring to the company"]
- [e.g., "Never speculates or gives opinions"]
- [e.g., "Uses emojis sparingly (max 1 per message)"]
- [e.g., "Structures responses with bullets for clarity"]

### Guardrails (Explicit "Do Nots")
[Critical safety and compliance component]
- [e.g., "Will not discuss pricing or contracts"]
- [e.g., "Will not answer questions outside knowledge domain"]
- [e.g., "Will not provide medical or legal advice"]
- [e.g., "Will not process payment information"]
- [e.g., "Will not share personal information about users"]

### Escalation Triggers
[Precise conditions for human handoff]
- User explicitly requests human agent
- User expresses frustration (sentiment score < -0.5)
- Same question asked 3 times without resolution
- Query involves sensitive topics [specify]
- Confidence score < 0.7 on response

### Key Functions
[Specific tasks persona performs successfully]
- Answer "how-to" questions
- Link to specific documentation
- Provide status of known system outages
- [Add specific capabilities]

### Example Interactions
[Provide 3-5 example Q&A pairs showing desired behavior]

**Example 1:**
- User: [Sample question]
- Persona: [Expected response]

**Example 2:**
- User: [Sample question]
- Persona: [Expected response]

**Example 3:**
- User: [Sample question that should escalate]
- Persona: [Expected escalation behavior]

### Persona Switching (if multi-persona system)
- **Trigger Keywords**: [List keywords that activate this persona]
- **Classification**: [Method for intent detection]
- **Announcement**: [How persona switch is communicated]
  - Example: "Switching you to our technical support specialist..."

### Acceptance Criteria

**Persona Consistency:**
- Score: ≥ 4/5 across 50 multi-turn conversations
- Method: Human evaluation using rubric (Appendix [X])

**Persona Classification Accuracy:**
- Target: ≥ 85% on 200-utterance labeled test set

**Guardrail Compliance:**
- Zero violations: 100% compliance on prohibited topics test set

**Escalation Accuracy:**
- Correct escalation: ≥ 95% on designated edge cases

**Persona Mixing:**
- Zero instances: No persona mixing within single response (100 test responses)

### Test Set
- **TaskSet**: [Name/Version, e.g., "TaskSet v2.0"]
- **Size**: [e.g., "300 interactions: 150 scripted + 150 freeform"]
- **Source**: [Client-provided and validated]

### Artifacts
- [ ] Persona prompt (versioned)
- [ ] Classification model/rules
- [ ] Test conversation transcripts
- [ ] Evaluation report
```

---

### **5.3 Agentic Use Case Specification Sheet**

Use this template for AI agents that perform autonomous tasks:

```markdown
## Agentic Use Case: [Use Case Name]

### Use Case Identification
- **Use Case ID**: [e.g., "AGENT-001"]
- **Complexity Tier**: [Tier 1 (Simple) / Tier 2 (Moderate) / Tier 3 (Complex)]
- **Version**: [e.g., "1.0"]

**Complexity Tier Definitions:**
- **Tier 1 (Simple)**: Single-step tool use, deterministic, <5 min execution
- **Tier 2 (Moderate)**: Multi-step (3-7 steps), simple conditional logic, 5-15 min execution
- **Tier 3 (Complex)**: Requires reasoning, planning, dynamic tool selection, >15 min execution

### Mission Statement
[Single, clear objective - the ultimate business outcome]
Example: "To process inbound email inquiries and draft a response for the 
correct account owner to review."

### Business Value
- **Problem Solved**: [What pain point does this address?]
- **ROI Hypothesis**: [Quantifiable benefit]
  - Example: "Reduce manual email triage time by 60%"
  - Example: "Increase response time SLA compliance from 70% to 95%"

### Workflow Definition

**Trigger(s):**
[Specific event(s) that initiate the workflow]
- [e.g., "New email arrives in support@company.com inbox"]
- [e.g., "New record created in Salesforce with status 'New'"]
- [e.g., "User clicks 'Process Invoice' button in UI"]

**Preconditions:**
[Systems, data, or states that must exist]
- [e.g., "Email contains valid sender address"]
- [e.g., "Salesforce API accessible"]
- [e.g., "User has appropriate permissions"]

**Main Success Flow:**
1. [Step 1: e.g., "Receive and parse incoming email"]
2. [Step 2: e.g., "Extract key entities (customer name, issue type)"]
3. [Step 3: e.g., "Search Salesforce for matching contact"]
4. [Step 4: e.g., "Classify issue type using NLU model"]
5. [Step 5: e.g., "Draft response using appropriate template"]
6. [Step 6: e.g., "Save draft to assignee's inbox"]
7. [Step N: e.g., "Log transaction in observability system"]

**Alternate/Failure Flows:**
- **If [condition]**: [Alternate action]
  - Example: "If contact not found in Salesforce: Flag email and escalate to human"
- **If [condition]**: [Alternate action]
  - Example: "If confidence < 0.7: Request human review before sending"

### Inputs
[Specific data fields required]
- `email_subject`: string
- `email_body`: string
- `sender_email`: string
- `received_timestamp`: datetime
- [Add all required input fields with types]

### Tools / Skills (Definitive List)
[APIs, functions, capabilities the agent can use]

**THIS IS THE CONTRACT:** If it's not listed here, the agent cannot do it.

1. **Tool Name**: `read_email(message_id: str)`
   - Description: Retrieves email content
   - Returns: Email object with subject, body, metadata

2. **Tool Name**: `search_salesforce_contact(email: str)`
   - Description: Searches for contact by email address
   - Returns: Contact record or null

3. **Tool Name**: `classify_intent(text: str)`
   - Description: Classifies query into predefined categories
   - Returns: Category label + confidence score

4. **Tool Name**: `generate_draft_response(template: str, context: dict)`
   - Description: Generates email draft
   - Returns: Draft email text

5. **Tool Name**: `save_to_drafts(recipient: str, subject: str, body: str)`
   - Description: Saves email to user's draft folder
   - Returns: Success boolean

[Add all tools with function signatures]

**Tool Permissions:**
- Read-only: [List tools with read-only access]
- Write: [List tools with write access]
- External API: [List external integrations]

**Autonomy Boundaries:**
- Agent MAY: [Allowed actions]
- Agent MAY NOT: [Prohibited actions, e.g., "Make payments", "Delete records"]

### Outputs
[Final, tangible artifacts produced]
- [e.g., "Draft email in Gmail 'Drafts' folder"]
- [e.g., "New Jira ticket with summary and priority"]
- [e.g., "Updated database record with processing status"]
- [e.g., "JSON log entry in observability system"]

### Success Criteria (Acceptance Metrics)

**Plan Completion Rate:**
- Target: ≥ 85%
- Definition: "Agent completes full workflow without manual intervention"
- Measured on: ScenarioSet v1.1 (n=100)

**Tool Success Rate:**
- Target: ≥ 90% per tool
- Definition: "Each tool call returns valid result"
- Measured on: ScenarioSet v1.1 (n=100)

**Step Efficiency:**
- Target: Median steps ≤ 8
- Definition: "Number of actions taken from trigger to completion"

**Task Success Rate (End-to-End):**
- Target: ≥ 80%
- Definition: "Correct output produced for test scenario"
- Measured on: 50-100 test scenarios

**Autonomy Boundary Violations:**
- Target: = 0
- Definition: "Attempts to call disallowed tools or actions"

**Performance:**
- **P95 Latency**: ≤ 6 seconds end-to-end
- **Cost per Transaction**: ≤ $0.25

**Rollback/Compensation:**
- If agent fails, system returns to safe state (define state)

### Failure Conditions & Handling
[How the agent behaves when it cannot complete]

**Failure Scenario 1**: [e.g., "Contact not found"]
- **Behavior**: [e.g., "Flag email in shared inbox, send Slack notification, take no further action"]

**Failure Scenario 2**: [e.g., "Low confidence in classification"]
- **Behavior**: [e.g., "Route to human review queue with explanation"]

**Failure Scenario 3**: [e.g., "API timeout"]
- **Behavior**: [e.g., "Retry with exponential backoff (3 attempts), then escalate"]

### Test Scenarios
- **ScenarioSet**: [Name/Version, e.g., "ScenarioSet v1.1"]
- **Size**: [e.g., "100 scenarios per orchestration"]
- **Composition**: [e.g., "70 happy path, 20 alternate path, 10 failure cases"]
- **Source**: [Client-validated or jointly created]

### Observability & Monitoring
- **Logging**: [What is logged - every tool call, decision point, timing]
- **Tracing**: [Span schema for distributed tracing]
- **Dashboard**: [Metrics displayed]
- **Alerts**: [Alert conditions]

### Security & Safety
- **Data Access**: [What data can agent read/write]
- **Rate Limits**: [API call limits]
- **Human-in-the-Loop**: [When required]
- **Audit Trail**: [What must be logged for compliance]

### Artifacts Delivered
- [ ] Workflow diagram (Visio/Lucidchart)
- [ ] Tool catalog with API specs
- [ ] Agent code/configuration
- [ ] ScenarioSet with test results
- [ ] Evaluation report with metrics
- [ ] Runbook for operations
- [ ] Dashboard for monitoring

### Explicitly Out of Scope
- [e.g., "Integration with systems not listed in Tools section"]
- [e.g., "Workflows requiring >10 steps"]
- [e.g., "Real-time learning or model updates"]
- [e.g., "Processing sensitive PII"]

### Timeline & Milestones
- Design Review: [Date]
- Tool Integration Complete: [Date]
- Testing Complete: [Date]
- Acceptance Run: [Date]
- Production Deployment: [Date]

### Sign-off
- Product Owner: [Name]
- AI Lead: [Name]
- Date: [Date]
```

---

### **5.4 Content Generation Specification Template**

Use this for projects where the primary deliverable is generated content:

```markdown
## Content Generation Specification: [Project Name]

### Content Goal
[Purpose and desired action]
Example: "Generate 5 engaging LinkedIn posts per week to drive traffic to our 
latest blog articles, targeting 500+ impressions and 50+ clicks per post."

### Target Audience
[Specific audience definition]
- **Role**: [e.g., "Chief Information Security Officers (CISOs)"]
- **Industry**: [e.g., "Mid-sized financial institutions ($500M-$5B revenue)"]
- **Knowledge Level**: [e.g., "Advanced technical understanding of cybersecurity"]
- **Motivations**: [e.g., "Reducing compliance risk, improving security posture"]

### Key Message
[Single most important takeaway]
Example: "Our new security platform reduces compliance risk by automating audit 
trails, enabling CISOs to achieve SOC 2 certification 40% faster."

### Tone & Style
[Define desired voice]
- [e.g., "Authoritative yet approachable"]
- [e.g., "Technical but not academic"]
- [e.g., "Urgent and action-oriented"]
- [e.g., "Professional, conversational"]

**Brand Guidelines**: [Link to style guide if available]

### Format & Structure

**Output Format:**
[Define exact structure]
- [e.g., "A 500-word blog post with:"]
  - Introduction (75 words)
  - 3 main points (each 125 words with sub-bullets)
  - Conclusion with call-to-action (50 words)
  - SEO title (60 characters max)
  - Meta description (155 characters max)

OR

- [e.g., "A JSON object with fields:"]
  ```json
  {
    "title": "string",
    "summary": "string (200 words max)",
    "keywords": ["string", "string", "string"],
    "main_content": "string",
    "call_to_action": "string"
  }
  ```

### Required Inputs
[Source material the model must use]
- [e.g., "The attached technical whitepaper (PDF)"]
- [e.g., "Transcript of CEO's keynote speech"]
- [e.g., "Product specifications document"]
- [e.g., "Competitor analysis report"]

### Constraints & Guardrails
[What content should NOT include]
- [e.g., "Do not mention competitors by name"]
- [e.g., "Avoid making specific pricing promises"]
- [e.g., "All statistics must be from the last 12 months"]
- [e.g., "Do not make medical or legal claims"]
- [e.g., "Avoid superlatives like 'best' or 'only'"]

### Quality Metrics

**Factual Accuracy:**
- Target: 99% of factual claims verifiable against source material
- Method: Human verification by SME

**Brand Alignment:**
- Target: Score ≥ 4/5 on brand voice alignment
- Method: Evaluated by marketing team using rubric (Appendix [X])

**Readability:**
- Target: Flesch Reading Ease score ≥ 60 (Grade 10 or lower)
- Method: Automated readability analysis

**Engagement Potential:**
- Target: [Specific metrics if measurable]
  - Example: "Predicted click-through rate ≥ 3%"
  - Example: "Sentiment score ≥ 0.6"

**SEO Optimization (if applicable):**
- Target keyword density: [e.g., "1-2%"]
- Meta description: [e.g., "155 characters, includes target keyword"]
- Header structure: [e.g., "H1, H2, H3 hierarchy maintained"]

### Evaluation Process
- **Test Set**: [e.g., "20 sample inputs with reference outputs"]
- **Human Evaluators**: [e.g., "3 marketing team members"]
- **Rubric**: [Link to detailed evaluation rubric]
- **Acceptance**: [e.g., "Average score ≥ 4/5 across all metrics"]

### Volume & Delivery
- **Quantity**: [e.g., "5 posts per week for 12 weeks = 60 total pieces"]
- **Schedule**: [Delivery cadence]
- **Review Process**: [Client review and approval workflow]

### Artifacts Delivered
- [ ] Generated content (all pieces)
- [ ] Source attribution log
- [ ] Quality metrics report
- [ ] Prompt templates (versioned)
- [ ] Generation pipeline documentation

### Explicitly Out of Scope
- [e.g., "Visual design or image generation"]
- [e.g., "Publication to social media platforms"]
- [e.g., "Real-time content updates or revisions"]
- [e.g., "Languages other than English"]

### Sign-off
- Content Owner: [Name]
- Approval Date: [Date]
```

---

## **6. Metrics & Acceptance Criteria Catalog**

This section provides a comprehensive catalog of metrics for different Gen AI capabilities. Always specify: **Metric + Dataset + Scoring Function + Threshold**.

### **6.1 Retrieval / RAG Metrics**

#### **Retrieval Quality Metrics**

**Recall@K**
- **Definition**: Fraction of queries where at least one relevant document appears in top-K results
- **Formula**: `(# queries with ≥1 relevant doc in top-K) / (total # queries)`
- **Typical Target**: ≥ 0.85 at K=5 or K=8
- **Use When**: Ensuring relevant information is retrieved

**Precision@K**
- **Definition**: Average proportion of relevant documents in top-K results
- **Formula**: `Σ (relevant docs in top-K) / (K × # queries)`
- **Typical Target**: ≥ 0.70 at K=5
- **Use When**: Reducing noise in retrieval

**Hit@K (Hit Rate)**
- **Definition**: Same as Recall@K
- **Use When**: Simpler terminology preferred

**Mean Reciprocal Rank (MRR)**
- **Definition**: Average of reciprocal ranks of first relevant document
- **Formula**: `(1/n) × Σ (1 / rank_of_first_relevant_doc)`
- **Typical Target**: ≥ 0.60
- **Use When**: Ranking quality matters (earlier = better)

**Coverage**
- **Definition**: Percentage of queries that return at least one document
- **Typical Target**: ≥ 0.95
- **Use When**: Ensuring system doesn't fail to retrieve

**Freshness Compliance**
- **Definition**: Percentage of retrieved documents meeting date/version requirements
- **Typical Target**: = 100% (for critical freshness policies)
- **Use When**: Time-sensitive information required

**Index Staleness**
- **Definition**: Maximum age of documents in index
- **Typical Target**: [Specified in freshness policy]
- **Use When**: Tracking data currency

#### **Answer Quality Metrics**

**Faithfulness / Groundedness**
- **Definition**: Degree to which answer is supported by retrieved context
- **Method**: LLM-judge rubric or human evaluation
- **Scale**: 0-1 or 1-5
- **Typical Target**: ≥ 0.90 (0-1 scale) or ≥ 4.0 (1-5 scale)
- **Use When**: Preventing hallucination
- **Template**: "On a scale of 1-5, is the answer fully supported by the provided context?"

**Source Attribution Rate**
- **Definition**: Percentage of answers that include at least one correct source citation
- **Typical Target**: ≥ 0.90
- **Use When**: Traceability required

**Relevance**
- **Definition**: Degree to which answer addresses the question
- **Method**: Human or LLM-judge evaluation
- **Scale**: 1-5
- **Typical Target**: ≥ 4.0
- **Use When**: Ensuring answers are on-topic

**Answer Correctness**
- **Definition**: Factual accuracy compared to ground truth
- **Method**: Human verification by SMEs
- **Typical Target**: ≥ 0.95
- **Use When**: Factual precision critical

**Exact Match (EM) / F1**
- **Definition**: Token-level overlap with reference answer
- **Typical Target**: EM ≥ 0.70, F1 ≥ 0.85
- **Use When**: Extractive QA with definitive answers

**Hallucination Rate**
- **Definition**: Percentage of answers containing unsupported claims
- **Method**: Human annotation or LLM-judge
- **Typical Target**: < 5% (ideally < 2%)
- **Use When**: High-stakes applications

#### **Performance Metrics**

**P95 Latency**
- **Definition**: 95th percentile response time
- **Typical Target**: ≤ 2.5 seconds (conversational) or ≤ 5 seconds (complex retrieval)
- **Use When**: User experience critical

**P50 Latency (Median)**
- **Definition**: Median response time
- **Typical Target**: ≤ 1.5 seconds
- **Use When**: Typical user experience

**Cost per Query**
- **Definition**: Average inference cost in USD
- **Typical Target**: ≤ $0.02 (varies by use case)
- **Use When**: Cost management required

**Throughput**
- **Definition**: Queries per second supported
- **Typical Target**: [Based on expected load]
- **Use When**: Scalability required

---

### **6.2 Conversational Assistant Metrics**

**Task Success Rate (TSR)**
- **Definition**: Percentage of user tasks completed successfully by the assistant
- **Typical Target**: ≥ 0.80
- **Measurement**: Human evaluation on task set
- **Use When**: Goal-oriented chatbots

**First Contact Resolution (FCR)**
- **Definition**: Percentage of inquiries resolved in first interaction without follow-up
- **Typical Target**: ≥ 0.70
- **Use When**: Support/service applications

**Containment Rate**
- **Definition**: Percentage of conversations handled without human escalation
- **Typical Target**: ≥ 0.75
- **Use When**: Automation ROI measurement

**Handoff Success Rate**
- **Definition**: When escalation triggered, percentage that successfully transfer to human
- **Typical Target**: ≥ 0.95
- **Use When**: Hybrid human-AI systems

**Persona Consistency**
- **Definition**: Degree to which responses match defined persona characteristics
- **Method**: Human evaluation using persona rubric
- **Scale**: 1-5
- **Typical Target**: ≥ 4.0
- **Use When**: Multi-persona systems

**Persona Classification Accuracy**
- **Definition**: Accuracy of routing queries to correct persona
- **Typical Target**: ≥ 0.85
- **Use When**: Multi-persona systems

**Safety Violations**
- **Definition**: Rate of responses violating safety policies
- **Typical Target**: ≤ 0.5% (or 0% for critical violations like PII exfiltration)
- **Use When**: All production systems

**Customer Effort Score (CES)**
- **Definition**: User-rated ease of interaction
- **Scale**: 1-7 (1 = very difficult, 7 = very easy)
- **Typical Target**: ≥ 5.0
- **Use When**: User experience measurement

**Time to First Token (TTFT)**
- **Definition**: Latency before first word appears
- **Typical Target**: ≤ 500ms
- **Use When**: Streaming responses

**Cost per Session**
- **Definition**: Average cost per complete conversation
- **Typical Target**: ≤ $0.10
- **Use When**: Budget constraints

---

### **6.3 Agentic Workflow Metrics**

**Plan Completion Rate**
- **Definition**: Percentage of workflows completed from trigger to output without human intervention
- **Typical Target**: ≥ 0.85
- **Use When**: Measuring autonomy

**Tool Success Rate**
- **Definition**: Success rate per tool/API call
- **Typical Target**: ≥ 0.90 per tool
- **Use When**: Identifying integration issues

**Step Efficiency**
- **Definition**: Median number of steps taken to complete workflow
- **Typical Target**: [Defined per use case, e.g., "≤ 8 steps"]
- **Use When**: Optimizing agent reasoning

**Task Success Rate**
- **Definition**: End-to-end success producing correct output
- **Typical Target**: ≥ 0.80
- **Use When**: Overall system quality

**Autonomy Boundary Violations**
- **Definition**: Attempts to call disallowed tools or perform prohibited actions
- **Typical Target**: = 0
- **Use When**: Safety and compliance

**Rollback/Compensation Success**
- **Definition**: Success rate of error recovery mechanisms
- **Typical Target**: ≥ 0.90
- **Use When**: Systems requiring transaction safety

**End-to-End Latency (P95)**
- **Definition**: Time from trigger to final output
- **Typical Target**: [Varies by use case, e.g., "≤ 6 seconds"]
- **Use When**: Performance requirements

**Cost per Transaction**
- **Definition**: Average cost to complete one workflow
- **Typical Target**: [Varies by use case, e.g., "≤ $0.25"]
- **Use When**: ROI calculation

---

### **6.4 Extraction / Classification Metrics**

**Extraction Metrics**

**Exact Match (EM) per Field**
- **Definition**: Percentage of fields extracted exactly correctly
- **Typical Target**: ≥ 0.80 per field
- **Use When**: Structured data extraction

**F1 Score per Field**
- **Definition**: Harmonic mean of precision and recall at token level
- **Typical Target**: ≥ 0.85 per field
- **Use When**: Partial matches acceptable

**Coverage**
- **Definition**: Percentage of documents where field is found
- **Typical Target**: [Varies by field prevalence]
- **Use When**: Ensuring completeness

**Confidence Calibration**
- **Definition**: Correlation between confidence scores and accuracy
- **Method**: Plot confidence vs. accuracy
- **Use When**: Building trust in predictions

**Classification Metrics**

**Macro F1**
- **Definition**: Average F1 across all classes (equal weight per class)
- **Typical Target**: ≥ 0.85
- **Use When**: Balanced class importance

**Weighted F1**
- **Definition**: F1 weighted by class frequency
- **Use When**: Imbalanced classes

**Per-Class Recall**
- **Definition**: Recall for each individual class
- **Typical Target**: [Varies by class importance, e.g., ≥ 0.90 for critical classes]
- **Use When**: Some classes more critical

**AUROC (Area Under ROC Curve)**
- **Definition**: Overall ranking quality
- **Typical Target**: ≥ 0.90
- **Use When**: Probabilistic outputs

---

### **6.5 Summarization Metrics**

**Faithfulness**
- **Definition**: Degree to which summary is factually consistent with source
- **Method**: Human or LLM-judge evaluation
- **Typical Target**: ≥ 0.90
- **Use When**: Factual accuracy critical

**Coverage**
- **Definition**: Percentage of key points from source included in summary
- **Method**: Human evaluation
- **Typical Target**: ≥ 0.85
- **Use When**: Completeness required

**Coherence**
- **Definition**: Logical flow and readability
- **Method**: Human evaluation using rubric
- **Scale**: 1-5
- **Typical Target**: ≥ 4.0
- **Use When**: User-facing summaries

**Compression Ratio**
- **Definition**: `(original length) / (summary length)`
- **Typical Target**: [Specified per use case, e.g., "10:1"]
- **Use When**: Length requirements exist

**Length Adherence**
- **Definition**: Percentage of summaries meeting length requirements
- **Typical Target**: ≥ 0.95
- **Use When**: Strict formatting needed

---

### **6.6 Non-Functional / Operational Metrics**

**Uptime SLO**
- **Definition**: Percentage of time system is operational
- **Typical Target**: ≥ 99.5% per month
- **Use When**: Production systems

**Error Budget**
- **Definition**: Allowable downtime per period
- **Use When**: SRE practices

**Mean Time to Recovery (MTTR)**
- **Definition**: Average time to restore service after failure
- **Typical Target**: [e.g., "< 15 minutes"]
- **Use When**: Incident response

**Security Compliance**
- **Definition**: Number of critical/high security findings
- **Typical Target**: 0 critical, 0 high
- **Use When**: Security assessments

**Data Residency Compliance**
- **Definition**: Percentage of data stored in approved regions
- **Typical Target**: = 100%
- **Use When**: Regulatory requirements

**Audit Trail Completeness**
- **Definition**: Percentage of transactions with complete logs
- **Typical Target**: = 100%
- **Use When**: Compliance and debugging

**Accessibility (WCAG) Compliance**
- **Definition**: WCAG conformance level
- **Typical Target**: AA or AAA
- **Use When**: UI components

---

### **6.7 Acceptance Criteria Template (Fill-in)**

Use this format for any deliverable:

```markdown
### Acceptance Criteria: [Deliverable Name]

**Evaluation Dataset:**
- Name: [e.g., "EvalSet v1.2"]
- Size: [e.g., "n=500"]
- Composition: [e.g., "Stratified by domain"]
- Source: [e.g., "Client SME-validated"]
- Storage: [Location]

**Model Configuration:**
- Model: [e.g., "gpt-4o"]
- Parameters: [e.g., "temperature=0.2, top_p=1"]
- Version: [Date or version string]

**Data Sources:**
- [List all data sources with versions]

**Environment:**
- [e.g., "Pre-Production", "Azure East US"]

**Metrics & Thresholds:**

| Metric | Threshold | Measurement Method |
|--------|-----------|-------------------|
| [Metric 1] | ≥/≤ [value] | [Method] |
| [Metric 2] | ≥/≤ [value] | [Method] |
| [Metric 3] | ≥/≤ [value] | [Method] |

**Acceptance Process:**
1. Single frozen evaluation run executed in [environment]
2. All metrics logged in [observability platform]
3. Results reviewed by [stakeholder name/role]
4. Acceptance report generated and attached
5. Client sign-off required by [date]

**Pass/Fail Criteria:**
- ALL metrics must meet or exceed thresholds
- Zero critical safety violations
- Complete documentation delivered
- [Add other binary criteria]
```

---

## **7. Evaluation Framework**

### **7.1 Evaluation Plan Components**

Every SOW must include a comprehensive evaluation plan addressing these components:

#### **7.1.1 Datasets**

**Dataset Specification:**
```markdown
**Dataset Name**: [e.g., "EvalSet v1.2"]
**Purpose**: [e.g., "Acceptance testing for RAG system"]
**Size**: [e.g., "500 examples"]
**Composition**: [e.g., "70% common queries, 20% edge cases, 10% failure cases"]
**Sampling Method**: [e.g., "Stratified random sampling across 5 domains"]
**Source**: [e.g., "Client SME-curated from 2000 historical queries"]
**Format**: [e.g., "JSONL with fields: question, answer, sources, metadata"]
**Storage Location**: [e.g., "Azure Blob Storage container 'eval-datasets'"]
**Access Control**: [e.g., "Client and vendor team only"]
**Leakage Checks**: [How to ensure no test data in training]
**Privacy Review**: [PII scrubbing procedures]
**Versioning**: [Semantic versioning, change log]
**Refresh Frequency**: [e.g., "Quarterly"]
```

**Dataset Types:**
- **Golden Set**: Ground truth for evaluation
- **Test Set**: Held-out data never seen during development
- **Validation Set**: For iterative improvement
- **Stress Test Set**: Edge cases and adversarial examples

#### **7.1.2 Annotation Process**

**When Human Annotation Required:**
- Creating ground truth labels
- Validating LLM-judge outputs
- Subjective quality assessment

**Annotation Specification:**
```markdown
**Rubric**: [Link to detailed rubric document]
**Scale**: [e.g., "1-5 Likert scale" or "Binary (correct/incorrect)"]
**Annotators**: [e.g., "3 client SMEs"]
**Training**: [e.g., "2-hour calibration session with examples"]
**Inter-Annotator Agreement (IAA)**:
  - **Target**: κ (Cohen's Kappa) ≥ 0.7
  - **Conflict Resolution**: [e.g., "Third annotator breaks ties"]
**Annotation Tool**: [e.g., "Label Studio"]
**Audit Trail**: [All annotations logged with timestamp and annotator ID]
**Sample Rubric**:

| Score | Definition | Example |
|-------|------------|---------|
| 5 | Fully faithful, comprehensive, actionable | [Example] |
| 4 | Mostly faithful, minor gaps | [Example] |
| 3 | Partially faithful | [Example] |
| 2 | Weakly grounded | [Example] |
| 1 | Hallucinated | [Example] |
```

#### **7.1.3 LLM-as-Judge**

**When to Use:**
- Scalable evaluation of large test sets
- Automated CI/CD quality checks
- Measuring subjective qualities (coherence, tone)

**Critical Requirements:**
```markdown
**Calibration**:
- LLM-judge must be validated against human labels on subset (n≥100)
- Report correlation coefficient (r ≥ 0.80 with human judgments)
- Document bias and variance

**LLM-Judge Configuration**:
- **Judge Model**: [e.g., "GPT-4o"]
- **Temperature**: [e.g., "0.0 for consistency"]
- **Prompt Version**: [Link to versioned prompt]
- **Rubric**: [Same rubric as human annotators]

**Quality Checks**:
- Periodic human validation (monthly or per release)
- Bias detection (consistent over-/under-scoring)
- Explanation quality (judge must provide reasoning)

**Transparency**:
- All judge prompts versioned and documented
- Judge scores logged alongside human scores for comparison
```

#### **7.1.4 Evaluation Runbook**

**Reproducibility Requirements:**
```markdown
**Environment**:
- Infrastructure: [e.g., "Azure Kubernetes, 4-core nodes"]
- Dependencies: [Pinned versions in requirements.txt]
- Random Seeds: [All seeds documented]

**Execution**:
- Command: `python evaluate.py --config eval_config_v1.2.yaml`
- Concurrency: [e.g., "Max 10 parallel requests"]
- Warmup: [e.g., "5 warmup queries before measurement"]
- Timeout: [e.g., "30s per query"]

**Data Flow**:
1. Load EvalSet from [location]
2. For each example:
   a. Call system with query
   b. Log input, output, latency, cost
   c. Compute metrics
3. Aggregate results
4. Generate report

**Output**:
- Metrics dashboard: [URL]
- Raw logs: [Azure Blob path]
- Report: [PDF/HTML location]
```

#### **7.1.5 Acceptance Sign-off Process**

```markdown
**Steps**:
1. **Pre-Acceptance Checklist**:
   - [ ] All code merged to main branch
   - [ ] EvalSet validated by client
   - [ ] Observability stack operational
   - [ ] Documentation complete

2. **Acceptance Run**:
   - Date/Time: [Scheduled]
   - Attendees: [Client SME, Vendor Tech Lead, PM]
   - Environment: Pre-Production (frozen)
   - Recording: [Session recorded for audit]

3. **Results Review**:
   - Metrics compared to thresholds (live dashboard)
   - Any failures investigated and documented
   - Baseline comparison (if exists)

4. **Sign-off**:
   - Client Product Owner approves in writing
   - Acceptance report attached to project documentation
   - Invoice trigger (if applicable)

**Dispute Resolution**:
- If metrics met but client disputes quality:
  - Third-party evaluation using agreed rubric
  - Mediation by [designated party]
  - Escalation path defined
```

---

### **7.2 Evaluation Artifacts (Deliverables)**

All evaluation plans must produce these artifacts:

- [ ] **Evaluation Harness Code** (executable, version-controlled)
- [ ] **Dataset Manifests** (all versions with metadata)
- [ ] **Rubric Documentation** (with examples and counterexamples)
- [ ] **Acceptance Report** (metrics, charts, analysis)
- [ ] **Replayable Run Configuration** (config files, seeds, commands)
- [ ] **Observability Logs** (raw data for audit)
- [ ] **Human Annotation Logs** (if applicable)

---

## **8. From Vague to Verifiable: Rewrite Examples**

This section provides before/after examples to illustrate the transformation from ambiguous to precise deliverables.

### **Example 1: RAG System**

#### ❌ **Vague (Bad)**
"RAG search with 95% accuracy"

**Problems:**
- What is being measured?
- What data?
- What method?
- No scope boundaries

#### ✅ **Contract-Ready (Good)**
"RAG-based Question Answering system on **EvalSet v1.2 (n=500 client-validated questions)** with:
- **Retrieval Recall@8 ≥ 0.85**
- **MRR ≥ 0.60**
- **Answer Faithfulness ≥ 0.90** (RAGAS metric)
- **Attribution Rate ≥ 0.90**
- **P95 Latency ≤ 2.5s**
- **Cost ≤ $0.02/query**

Using **Model: GPT-4o with temperature=0.2** indexing **SharePoint Sites A,B and Confluence Space C**. Single frozen acceptance run recorded in **Azure AI Foundry** observability platform."

---

### **Example 2: Chatbot with Personas**

#### ❌ **Vague (Bad)**
"Chatbot with 2 personas"

**Problems:**
- What defines a persona?
- How are they different?
- How is quality measured?
- What can/can't it do?

#### ✅ **Contract-Ready (Good)**
"Conversational assistant supporting **Persona A (Customer Support)** and **Persona B (Sales Advisor)** with complete persona specification cards (see Appendix A, B) defining:
- Distinct knowledge domains, tone, behaviors, and guardrails per persona
- Persona classification accuracy ≥ 85% on labeled test set
- Persona consistency score ≥ 4/5 by human evaluation

Evaluated on **TaskSet v2.0 (n=300: 150 customer support, 150 sales scenarios)** achieving:
- **Task Success Rate ≥ 0.80**
- **Containment Rate ≥ 0.75**
- **Safety violations ≤ 0.5%**
- **P95 Latency ≤ 2.0s per turn**

Persona prompts versioned and guardrails documented. Zero instances of persona mixing in 100-response test set."

---

### **Example 3: Agentic Use Cases**

#### ❌ **Vague (Bad)**
"Build 3 agentic use cases"

**Problems:**
- What is a "use case"?
- How complex?
- What defines success?
- What tools/integrations?

#### ✅ **Contract-Ready (Good)**
"Three validated autonomous agent workflows (Invoice Processing, Customer Onboarding, IT Ticket Triage) each with:

**Per Use Case:**
- Complete specification sheet (see Section 5.3 template)
- Business process flow diagram
- Definitive tool catalog (5-8 tools per agent)
- ScenarioSet (n=100) for acceptance testing

**Acceptance Criteria per Workflow:**
- **Plan Completion Rate ≥ 0.85** (autonomous end-to-end)
- **Tool Success Rate ≥ 0.90** per individual tool
- **Task Success Rate ≥ 0.80** (correct output)
- **Median Steps ≤ 8**
- **Autonomy Boundary Violations = 0**
- **P95 Latency ≤ 6s**
- **Cost/transaction ≤ $0.25**

**Deliverables per Use Case:**
- Flow diagram (Lucidchart)
- Agent code/configuration
- Evaluation report with metrics
- Demo script
- Operations runbook"

---

### **Example 4: Accuracy Improvement**

#### ❌ **Vague (Bad)**
"Improve accuracy"

**Problems:**
- Improve from what baseline?
- By how much?
- On what metric?
- At what cost?

#### ✅ **Contract-Ready (Good)**
"Increase **Answer Faithfulness** from current baseline of **0.82 to ≥ 0.90** on **EvalSet v1.2** without:
- Reducing **Retrieval Recall@8 below 0.80**
- Increasing **P95 latency above 3.0s**
- Increasing **cost/query above $0.025**

**Method:**
- Implement semantic reranker
- Optimize prompt engineering
- Add citation verification step

**Validation:**
- Single frozen acceptance run comparing baseline vs. improved system
- Both runs on identical EvalSet v1.2
- Results logged in observability dashboard"

---

### **Example 5: Content Generation**

#### ❌ **Vague (Bad)**
"Generate high-quality marketing content"

**Problems:**
- What constitutes "high quality"?
- What format?
- How much content?
- What's the review process?

#### ✅ **Contract-Ready (Good)**
"Generate **60 LinkedIn posts** (5 per week for 12 weeks) targeting CISOs in financial services, each post:

**Format:**
- 150-250 words
- 1 compelling headline
- 3 key points
- 1 call-to-action with link
- 3-5 relevant hashtags

**Quality Metrics:**
- **Factual Accuracy**: 99% of claims verifiable against source whitepapers
- **Brand Alignment**: ≥ 4/5 score by marketing team using brand rubric (Appendix C)
- **Readability**: Flesch Reading Ease ≥ 60
- **SEO**: Target keyword density 1-2%

**Evaluation:**
- Test batch: 20 posts evaluated before full production
- Human review: 3 marketing team members per rubric
- Revision allowance: Up to 2 rounds of revisions per post

**Deliverables:**
- All 60 posts (Google Docs)
- Source attribution log
- Quality metrics report
- Prompt templates (versioned)"

---

### **8.1 Quick Reference: Red Flags → Fixes**

| ❌ Red Flag (Vague) | ✅ Fix (Specific) |
|---------------------|-------------------|
| "High accuracy" | "F1 score ≥ 0.85 on 1,000-example client test set" |
| "Intelligent routing" | "Classifies into 5 categories with ≥ 90% precision, evaluated on 500-ticket test set" |
| "Natural conversations" | "Handles 10+ turn conversations maintaining context, evaluated on 50 test dialogues with ≥ 4/5 coherence rating" |
| "Real-time processing" | "P95 latency ≤ 2 seconds under 50 concurrent user load" |
| "Comprehensive documentation" | "API reference, integration guide with 5 code examples, troubleshooting guide - minimum 25 pages" |
| "Enterprise-grade" | "99.5% uptime, SOC 2 compliant infrastructure, supports 1000 concurrent users" |
| "Custom AI model" | "Fine-tuned GPT-4 on 1,000 client examples, ≥ 20% F1 improvement over base model on held-out test set" |
| "Agentic workflow" | "Autonomous 7-step workflow with 4 decision points, 80% completion rate on 100-scenario test set" |

---

## **9. SOW Structure & Required Appendices**

### **9.1 Mandatory SOW Sections**

Every GenAI SOW must contain:

#### **Section 1: Executive Summary**
- Project objectives and business value
- High-level scope
- Key success metrics
- Timeline and budget overview

#### **Section 2: Scope of Work**
- Detailed deliverable specifications (using templates from Section 5)
- Clear in-scope / out-of-scope boundaries
- Dependencies and assumptions
- Client vs. vendor responsibilities

#### **Section 3: Technical Architecture**
- System components and data flow
- Model and technology stack
- Infrastructure requirements
- Integration points

#### **Section 4: Evaluation Plan**
- Dataset specifications
- Metrics and thresholds
- Acceptance criteria
- Testing methodology

#### **Section 5: Data & Privacy**
- Data sources and access
- Data governance
- Privacy and security requirements
- Compliance obligations

#### **Section 6: Delivery Schedule**
- Milestones with dates
- Dependencies and critical path
- Review and approval points
- Acceptance timeline

#### **Section 7: Governance & Change Control**
- Project governance structure (RACI)
- Change request process
- Escalation procedures
- Risk management

#### **Section 8: Support & Maintenance**
- Warranty period
- Support SLAs (if applicable)
- Handover process
- Knowledge transfer

### **9.2 Mandatory Appendices**

#### **Appendix A: Glossary of Terms**
Project-specific definitions of all ambiguous terms:

```markdown
**Accuracy**: In this project, refers to Answer Faithfulness (see Appendix B 
for rubric), not retrieval accuracy or other metrics.

**Use Case**: A complete business workflow from trigger to verified output, 
with defined success metrics (see Use Case Template in Section 5.3).

**Persona**: A distinct conversational identity with specific knowledge domain, 
tone, behaviors, and guardrails as defined in Persona Specification Card 
(see Section 5.2).

**Acceptance**: Client sign-off based on single frozen evaluation run meeting 
all thresholds defined in Section 4.

[Add all project-specific terms]
```

#### **Appendix B: Evaluation Rubrics**
Detailed scoring criteria for any human evaluation:

```markdown
## Answer Faithfulness Rubric

**Scale**: 1-5

**5 - Fully Faithful**
- All claims directly supported by retrieved context
- No speculation or unsupported inferences
- Exact citations provided
- Example: [Provide example]

**4 - Mostly Faithful**
- Primary claims supported, minor unsupported details
- Appropriate hedging used
- Citations provided for main points
- Example: [Provide example]

**3 - Partially Faithful**
- Some claims supported, some not
- Mix of grounded and speculative content
- Incomplete citations
- Example: [Provide example]

**2 - Weakly Grounded**
- Minimal support from context
- Mostly speculation
- Few or no citations
- Example: [Provide example]

**1 - Hallucinated**
- Claims contradict or ignore context
- Fabricated information
- No valid citations
- Example: [Provide example]
```

#### **Appendix C: Test Datasets**

```markdown
## EvalSet v1.2 Specification

**Purpose**: Acceptance testing for RAG system

**Composition**:
- Total Examples: 500
- Breakdown:
  - Product FAQs: 150 (30%)
  - Technical Documentation: 150 (30%)
  - Policy Questions: 100 (20%)
  - Edge Cases: 75 (15%)
  - Failure Cases: 25 (5%)

**Format**:
```json
{
  "question_id": "Q001",
  "question": "How do I reset my password?",
  "answer_reference": "Navigate to Settings > Security > Reset Password...",
  "source_documents": ["doc_123", "doc_456"],
  "domain": "product_faq",
  "difficulty": "easy"
}
```

**Creation Process**:
- Curated by [Client SME team] from [source]
- Validated by [Process]
- Inter-annotator agreement: κ = 0.82

**Storage**: Azure Blob Storage: `eval-datasets/evalset_v1.2.jsonl`

**Access**: [Client and vendor team only, access control defined]

**Version Control**: Semantic versioning; any change = new version = change order
```

#### **Appendix D: Example Interactions**

```markdown
## Persona A: Technical Support - Example Interactions

**Example 1: Successful Resolution**

User: "My dashboard isn't loading. What should I do?"
Persona Response: "I'll help you troubleshoot the dashboard loading issue. Let me guide you through some steps:

1. First, try clearing your browser cache and refreshing the page
2. If that doesn't work, check if you can access other pages in the application
3. Verify your internet connection is stable

If none of these resolve the issue, I can escalate this to our technical team. Would you like to try these steps first, or shall I create a support ticket for you?"

**Analysis**: 
- ✅ Professional, helpful tone
- ✅ Provides structured troubleshooting steps
- ✅ Offers escalation path
- ✅ Asks clarifying question

**Example 2: Out-of-Scope Query**

User: "Can you give me a discount on my subscription?"

Persona Response: "I appreciate your interest in our pricing! However, I'm focused on technical support and don't have access to billing or pricing discussions. I'd be happy to connect you with our sales team who can discuss your subscription options and any available discounts. Would you like me to create a referral for you?"

**Analysis**:
- ✅ Polite acknowledgment
- ✅ Clear boundary statement (guardrail)
- ✅ Offers appropriate handoff
- ✅ Maintains helpful tone

**Example 3: Escalation Trigger**

User: "This is ridiculous! I've been trying to fix this for hours and nothing works!"

Persona Response: "I understand your frustration, and I apologize for the difficulty you're experiencing. This sounds like it requires more immediate attention than I can provide. Let me connect you with a senior technical specialist who can prioritize your issue. 

I'm transferring your conversation now. They'll have access to our chat history and will reach out within 15 minutes. Is there anything else I should pass along to them about your situation?"

**Analysis**:
- ✅ Acknowledges frustration (escalation trigger)
- ✅ Takes ownership and apologizes
- ✅ Clearly explains escalation
- ✅ Sets expectation for response time
- ✅ Offers to gather additional context
```

#### **Appendix E: Integration Specifications**

```markdown
## API Specifications

### RAG Query API

**Endpoint**: `POST /api/v1/rag/query`

**Authentication**: Bearer token (OAuth 2.0)

**Rate Limits**: 100 requests per minute per API key

**Request Schema**:
```json
{
  "query": "string (required, max 500 chars)",
  "context": {
    "user_id": "string (optional)",
    "session_id": "string (optional)",
    "domain": "string (optional, enum: [product, policy, technical])"
  },
  "options": {
    "max_tokens": "integer (optional, default: 500, max: 2000)",
    "temperature": "float (optional, default: 0.2, range: 0-1)",
    "top_k": "integer (optional, default: 8, max: 20)",
    "include_sources": "boolean (optional, default: true)"
  }
}
```

**Response Schema**:
```json
{
  "query_id": "string (UUID)",
  "answer": "string",
  "sources": [
    {
      "document_id": "string",
      "title": "string",
      "url": "string",
      "relevance_score": "float (0-1)",
      "excerpt": "string"
    }
  ],
  "confidence": "float (0-1)",
  "latency_ms": "integer",
  "metadata": {
    "model_version": "string",
    "timestamp": "ISO 8601 datetime"
  }
}
```

**Error Responses**:
- `400 Bad Request`: Invalid query format
- `401 Unauthorized`: Invalid or missing authentication
- `429 Too Many Requests`: Rate limit exceeded
- `500 Internal Server Error`: System error
- `503 Service Unavailable`: System maintenance

**Example Request** (cURL):
```bash
curl -X POST https://api.example.com/v1/rag/query \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "How do I reset my password?",
    "options": {
      "include_sources": true
    }
  }'
```

### Integration Documentation Deliverables:
- [ ] OpenAPI 3.0 specification (YAML)
- [ ] Postman collection with examples
- [ ] Code examples (Python, JavaScript, cURL)
- [ ] Error handling guide
- [ ] Authentication setup guide
```

#### **Appendix F: Success Criteria Summary (One-Page Checklist)**

```markdown
## Acceptance Criteria Checklist: [Project Name]

**Evaluation Dataset**: EvalSet v1.2 (n=500)
**Model Configuration**: GPT-4o, temp=0.2, top_p=1
**Environment**: Pre-Production
**Acceptance Date**: [Date]

### Functional Requirements
- [ ] System accepts queries via API endpoint
- [ ] Returns answers with source citations
- [ ] Handles all data sources (SharePoint A, B, Confluence C)
- [ ] Supports concurrent queries (10 users)

### Performance Metrics
- [ ] Retrieval Recall@8 ≥ 0.85
- [ ] MRR ≥ 0.60
- [ ] Answer Faithfulness ≥ 0.90
- [ ] Attribution Rate ≥ 0.90
- [ ] P95 Latency ≤ 2.5s
- [ ] Cost/query ≤ $0.02

### Quality Metrics
- [ ] Hallucination Rate < 5%
- [ ] Citation Coverage ≥ 90%
- [ ] Relevance Score ≥ 4.0/5.0

### Security & Compliance
- [ ] PII redaction pipeline operational
- [ ] Zero critical security findings (pen test)
- [ ] Data residency compliance (US East)
- [ ] Audit logging enabled

### Observability
- [ ] Langfuse monitoring configured
- [ ] Dashboard accessible to client
- [ ] Alerts configured for latency, cost, errors
- [ ] All queries logged with trace IDs

### Documentation
- [ ] Architecture diagram delivered
- [ ] API documentation complete
- [ ] User guide delivered
- [ ] Operations runbook delivered
- [ ] Evaluation report attached

### Sign-off
- [ ] Client Product Owner: _________________ Date: _______
- [ ] Vendor Tech Lead: _________________ Date: _______
- [ ] Project Manager: _________________ Date: _______

**Pass/Fail**: [PASS / FAIL]
**Notes**: [Any observations or exceptions]
```

#### **Appendix G: Architecture Diagrams**

Include system architecture diagrams showing:
- Data flow (from sources through retrieval to generation)
- Component interactions
- Infrastructure setup
- Integration points
- Security boundaries

#### **Appendix H: RACI Matrix**

```markdown
## RACI: Generative AI Project Governance

| Activity | Product Owner | AI Lead | Data Eng | Sec/Privacy | SRE | Vendor |
|----------|---------------|---------|----------|-------------|-----|--------|
| Use case definition | A | R | C | C | I | C |
| Dataset governance | C | R | A | R | I | C |
| Evaluation & acceptance | A | R | C | C | I | R |
| Prompt/model versioning | C | R | I | C | I | R |
| Data pipeline development | C | C | A | C | I | R |
| Security & privacy review | C | C | C | A | C | C |
| Production deployment | C | C | C | C | A | R |
| Incident response | I | C | C | C | A | R |
| Client communication | A | C | I | I | I | R |

**Legend**:
- **R** = Responsible (does the work)
- **A** = Accountable (final authority, signs off)
- **C** = Consulted (provides input)
- **I** = Informed (kept in the loop)
```

---

## **10. Governance & Review Process**

### **10.1 Four-Stage Gate Process**

#### **Gate 1: Pre-SOW Technical Review**
**Purpose**: Ensure technical feasibility and measurability before client commitment

**Required Artifacts**:
- [ ] Draft deliverable specifications (using Section 5 templates)
- [ ] Proposed metrics and thresholds
- [ ] Evaluation plan outline
- [ ] Technical risk assessment

**Review Panel**:
- Solutions Architect (required)
- AI/ML SME (required)
- Project Manager (required)
- Security/Privacy SME (if applicable)

**Approval Criteria**:
- All metrics are measurable with defined methodology
- Evaluation datasets can be created/obtained
- Technical approach is sound
- Risks identified with mitigation plans
- Client responsibilities clearly defined

**Outcome**: GO / NO-GO / REVISE

---

#### **Gate 2: Design Phase Review**
**Purpose**: Validate that implementation plans align with SOW commitments

**Required Artifacts**:
- [ ] Detailed architecture diagram
- [ ] Complete evaluation plan with datasets
- [ ] Observability and logging plan
- [ ] Security and compliance assessment
- [ ] Test scenarios for all use cases

**Review Panel**:
- Technical Architect (required)
- AI Lead (required)
- Data Engineer (required)
- Client Product Owner (required)

**Approval Criteria**:
- Architecture supports all deliverable requirements
- All test datasets defined and validated by client
- Observability plan covers all required metrics
- Security controls documented
- Timeline and milestones realistic

**Outcome**: PROCEED / HOLD / REDESIGN

---

#### **Gate 3: Pre-UAT Review**
**Purpose**: Confirm readiness for client acceptance testing

**Required Artifacts**:
- [ ] All code complete and merged
- [ ] Evaluation results on validation set
- [ ] Observability dashboard operational
- [ ] Documentation complete (user, admin, API)
- [ ] Client-approved acceptance test plan

**Review Panel**:
- AI Lead (required)
- Project Manager (required)
- Client Product Owner (required)
- QA/Testing Lead (required)

**Approval Criteria**:
- All metrics achieved on internal validation set
- No critical bugs or security issues
- Documentation reviewed and approved
- Acceptance test environment ready
- Client has validated EvalSet and rubrics

**Outcome**: READY FOR UAT / NOT READY

---

#### **Gate 4: Post-Go-Live Review**
**Purpose**: Validate production performance and capture lessons learned

**Timeline**: Within 30 days of production deployment

**Required Artifacts**:
- [ ] Acceptance test report (signed)
- [ ] Production metrics report (first 30 days)
- [ ] Incident log and resolution summary
- [ ] Lessons learned document
- [ ] Reusable assets for knowledge base

**Review Panel**:
- Project Manager (required)
- AI Lead (required)
- Client Product Owner (required)
- Operations/SRE (if applicable)

**Approval Criteria**:
- Live metrics meet acceptance thresholds
- No unresolved critical issues
- Client satisfaction confirmed
- Knowledge transfer complete
- Deliverables catalogued for reuse

**Outcome**: PROJECT CLOSED / SUPPORT TRANSITION COMPLETE

---

### **10.2 Change Control Process**

#### **Triggers for Change Order**

Any modification to the following requires a formal change order:

**Scope Changes**:
- Data sources added or removed
- Additional use cases or personas
- New tools or integrations
- Expanded language support
- Additional environments (dev, staging, prod)

**Technical Changes**:
- Dataset version changes (EvalSet updated)
- Model or provider changes (e.g., GPT-4 → Claude)
- Threshold changes (metric targets adjusted)
- Schema changes (API, data formats)

**Requirement Changes**:
- New SLAs or performance requirements
- Additional security/compliance requirements
- Expanded user base or load requirements
- New regulatory requirements

#### **Change Request Template**

```markdown
## Change Request: [CR-ID]

**Requested By**: [Name, Role]
**Date**: [Date]
**Priority**: [Critical / High / Medium / Low]

### Description of Change
[Clear description of what needs to change and why]

### Business Justification
[Why is this change needed? What is the impact if not implemented?]

### Impact Analysis

**Scope Impact**:
- Deliverables affected: [List]
- New deliverables: [List]
- Removed deliverables: [List]

**Technical Impact**:
- Architecture changes required: [Yes/No, describe]
- New integrations needed: [Yes/No, list]
- Performance implications: [Describe]

**Schedule Impact**:
- Additional time required: [X weeks]
- Affected milestones: [List]
- New target dates: [List]

**Cost Impact**:
- Additional budget required: [$X]
- Cost breakdown: [Detail]

**Risk Impact**:
- New risks introduced: [List]
- Mitigation strategies: [Describe]

### Evaluation Impact
- [ ] Requires new/updated test dataset
- [ ] Requires new metrics or thresholds
- [ ] Requires re-evaluation of existing deliverables
- [ ] Affects acceptance criteria

### Approval
- [ ] Client Product Owner: _________________ Date: _______
- [ ] Vendor Project Manager: _________________ Date: _______
- [ ] Technical Lead: _________________ Date: _______

**Decision**: [APPROVED / REJECTED / DEFERRED]
**Revised SOW Section**: [Reference to updated SOW sections]
```

---

### **10.3 Out-of-Scope Examples (Standard Exclusions)**

Include these in every SOW to set clear boundaries:

**Data & Content**:
- Additional data sources not explicitly listed
- Real-time data synchronization (unless specified)
- Complete data cleanup or Master Data Management
- Content moderation beyond defined guardrails
- Historical data migration or backfilling

**Infrastructure & Operations**:
- Enterprise SSO rollout or identity management
- Multi-region deployment (unless specified)
- Disaster recovery beyond defined RTO/RPO
- 24/7 on-call support (unless specified)
- Production monitoring beyond observability stack

**Customization & Expansion**:
- Unlimited prompt tuning or optimization
- Model retraining or fine-tuning (unless specified)
- Additional languages beyond those listed
- Mobile app development
- UI/UX design or frontend development

**Integration & Downstream**:
- Downstream system refactoring
- Business process redesign
- Change management or training programs
- Staffing of human agents
- Customer success or adoption programs

**Ongoing Services**:
- Continuous model improvement (unless specified)
- Content generation beyond defined volume
- Ongoing dataset curation
- Regular security audits (unless specified)

---

## **11. Implementation Guide**

### **11.1 For Sales Teams**

#### **Pre-Sales Discovery**

**Week 1-2: Initial Engagement**
1. **Understand Business Problem**:
   - What business outcome is the client trying to achieve?
   - What metrics will demonstrate success?
   - What are the constraints (time, budget, data, regulations)?

2. **Assess Technical Feasibility**:
   - Involve Solutions Architect in discovery calls
   - Evaluate data availability and quality
   - Identify integration requirements
   - Document assumptions and risks

3. **Set Realistic Expectations**:
   - Use examples from Section 8 to show precision
   - Explain iterative nature of AI development
   - Discuss evaluation methodology upfront
   - Share timelines for similar past projects

**Week 3-4: Scoping Workshop**

**Mandatory: Definition Workshop (2-4 hours with client)**

This is a value-add activity that demonstrates expertise and prevents future disputes.

**Agenda**:
1. **Review S.M.A.R.T.A.I. Framework** (30 min)
   - Educate client on importance of precision
   - Walk through framework components

2. **Define Deliverables Using Templates** (90-120 min)
   - Use Section 5 templates
   - Fill out specifications collaboratively
   - Document in real-time (shared screen)
   - Capture client terminology and definitions

3. **Co-create Evaluation Plan** (45-60 min)
   - Define metrics and thresholds together
   - Discuss test dataset creation
   - Agree on acceptance process
   - Document client responsibilities

4. **Document Out-of-Scope** (30 min)
   - Explicitly state what's NOT included
   - Prevent future scope creep
   - Define change control process

**Outputs**:
- Draft deliverable specifications (using templates)
- Agreed metrics and thresholds
- Client-validated evaluation plan
- Glossary of terms
- List of assumptions and dependencies

**Week 5: SOW Finalization**

1. **Internal Technical Review**:
   - Submit to Gate 1 review panel
   - Address feasibility concerns
   - Validate metrics are measurable
   - Confirm resource requirements

2. **Create SOW Document**:
   - Use structure from Section 9
   - Include all mandatory appendices
   - Reference workshop outputs
   - Ensure traceability

3. **Client Review**:
   - Walk through SOW with client
   - Confirm alignment with workshop
   - Address questions
   - Obtain sign-off

#### **Sales Toolkit**

**Use these resources in sales process**:

1. **One-Page TL;DR** (Section 0 from Document 2):
   - Handout for initial client meetings
   - Establishes credibility
   - Sets expectations for precision

2. **Example Rewrites** (Section 8):
   - Show before/after transformations
   - Demonstrate your rigor
   - Build confidence

3. **S.M.A.R.T.A.I. Checklist**:
   - Use in discovery calls
   - Ensure all criteria covered
   - Document gaps

4. **Metrics Catalog** (Section 6):
   - Reference during scoping
   - Educate clients on options
   - Build shared vocabulary

#### **Common Sales Objections & Responses**

**Objection**: "This level of detail seems like overkill. Can't we just get started?"

**Response**: "I completely understand the desire to move quickly. However, in our experience, projects that lack this precision at the outset encounter significant delays and cost overruns later. The 2-3 weeks we invest now in defining exact success criteria will save 2-3 months of rework and disputes during delivery. Our track record shows that projects with clear deliverables have 40% faster acceptance and 60% fewer change orders. Would you prefer to invest time upfront or deal with ambiguity during delivery?"

**Objection**: "Your competitors quoted this much simpler and faster."

**Response**: "That's an important consideration. I'd encourage you to ask them specifically how they'll measure success. What exact metrics will they use? What test dataset? How will you know when it's done? If they can't answer these questions precisely, you're at risk of a project that's perpetually 'almost done' but never acceptable. We're positioning ourselves as the mature, reliable AI partner who delivers predictable outcomes. The clarity we provide isn't overhead—it's how we de-risk your investment."

**Objection**: "We want to use Agile/iterative development. This feels too rigid."

**Response**: "Excellent point. These specifications aren't rigid waterfall requirements—they're the target we're iterating toward. In each sprint, we'll measure progress against these defined metrics. The evaluation framework gives us rapid feedback loops. What we're eliminating is ambiguity about the destination, not flexibility in how we get there. We'll iterate on prompts, data processing, and models, but we'll always know if we're making progress because we've defined what 'better' means."

---

### **11.2 For Project Managers**

#### **Project Setup (Week 1)**

1. **Gate 1 Review**:
   - Facilitate technical review
   - Document approvals and conditions
   - Address any concerns before kickoff

2. **Establish Communication Cadence**:
   - Weekly status meetings
   - Demo schedule (every 2 weeks recommended)
   - Escalation procedures
   - Decision log

3. **Create Project Artifacts**:
   - Project charter referencing SOW
   - RACI matrix (use Appendix H template)
   - Risk register
   - Issue log

#### **During Execution**

1. **Reference SOW in Every Status Update**:
   - Track progress against specific acceptance criteria
   - Use metrics dashboard as discussion focal point
   - Flag any deviations from plan immediately

2. **Manage Scope Actively**:
   - Log all change requests (use Section 10.2 template)
   - Assess impact before agreeing
   - Document client requests outside scope
   - Initiate change order process when needed

3. **Track Dependencies**:
   - Monitor client-provided artifacts (data, test sets, approvals)
   - Escalate delays impacting critical path
   - Document assumptions when dependencies unclear

4. **Prepare for Gate Reviews**:
   - Maintain checklist of gate requirements
   - Gather artifacts progressively
   - Don't wait until last minute
   - Schedule reviews with adequate lead time

#### **Pre-Acceptance (2 weeks before)**

1. **Gate 3 Review**:
   - Confirm all artifacts ready
   - Validate metrics on validation set
   - Ensure documentation complete
   - Verify acceptance environment

2. **Coordinate Acceptance Run**:
   - Schedule with all stakeholders
   - Prepare live dashboard
   - Test run-through internally
   - Have backup plan for technical issues

3. **Finalize Documentation**:
   - Acceptance report template prepared
   - All appendices updated
   - Architecture diagram final version
   - Runbooks reviewed

#### **Acceptance & Closure**

1. **Facilitate Acceptance Run**:
   - Record session (with permission)
   - Walk through dashboard live
   - Address questions immediately
   - Document any observations

2. **Obtain Sign-off**:
   - Use checklist from Appendix F
   - Get signatures on acceptance report
   - Trigger invoicing (if applicable)
   - Celebrate with team!

3. **Post-Go-Live Activities**:
   - Monitor production metrics
   - Address any initial issues
   - Schedule Gate 4 review
   - Capture lessons learned

4. **Knowledge Management**:
   - Upload reusable artifacts to internal knowledge base
   - Tag with capabilities, industry, use case
   - Document lessons learned
   - Share success story internally

---

### **11.3 For Engineering Teams**

#### **Development Best Practices**

1. **Challenge Vague Requirements Early**:
   - Don't start work on ambiguous deliverables
   - Push back to PM/sales with specific questions
   - Reference this guide's templates
   - Document assumptions if forced to proceed

2. **Propose Measurement Methodologies**:
   - Suggest specific metrics from Section 6
   - Build evaluation harness early (parallel to development)
   - Test metrics on small datasets first
   - Get client validation on measurement approach

3. **Version Everything**:
   - Code: Git with semantic versioning
   - Prompts: Version-controlled prompt library
   - Datasets: Versioned with change logs
   - Models: Track provider, model, version, parameters
   - Configs: All settings in version control

4. **Build Observability from Day 1**:
   - Instrument logging before writing business logic
   - Track every LLM call (input, output, latency, cost)
   - Use structured logging (JSON)
   - Create dashboards early

5. **Document Limitations Honestly**:
   - If something won't work in production like it did in demo, communicate immediately
   - Document edge cases where system fails
   - Provide realistic performance expectations
   - Don't over-promise

#### **Evaluation Development**

1. **Build Test Harness First**:
   - Create evaluation pipeline before or during development
   - Make it easy to run (one command)
   - Automate as much as possible
   - Include in CI/CD if feasible

2. **Create Multiple Test Sets**:
   - **Dev Set**: For rapid iteration (small, fast)
   - **Validation Set**: For tuning (medium size)
   - **Test Set**: For acceptance (frozen, client-validated)
   - **Stress Test Set**: Edge cases and adversarial examples

3. **Validate Metrics Early**:
   - Test metric calculation on known examples
   - Verify LLM-judge against human labels
   - Check for bugs in evaluation code
   - Get client feedback on sample results

4. **Track Progress Continuously**:
   - Run evaluation on every major change
   - Plot metrics over time
   - Share results with PM/client regularly
   - Identify regressions early

#### **Pre-Delivery Checklist**

Before submitting for acceptance:

- [ ] **Functionality**:
  - All specified capabilities implemented
  - Integration tests passing
  - Error handling comprehensive

- [ ] **Performance**:
  - Latency measured and within thresholds
  - Cost per query within budget
  - Load tested at expected concurrency

- [ ] **Evaluation**:
  - All metrics computed on test set
  - Results meet or exceed thresholds
  - Evaluation report generated
  - Metrics dashboard operational

- [ ] **Observability**:
  - Logging enabled and tested
  - Dashboard accessible to client
  - Alerts configured
  - Trace IDs present on all logs

- [ ] **Security**:
  - Security scan completed (no critical findings)
  - PII handling validated
  - Access controls tested
  - Audit logging enabled

- [ ] **Documentation**:
  - Architecture diagram updated
  - API documentation complete and tested
  - User guide written
  - Operations runbook complete
  - Code comments sufficient

- [ ] **Artifacts**:
  - All deliverable artifacts ready
  - Evaluation datasets stored and documented
  - Prompt library versioned
  - Configuration files included

---

### **11.4 For Client Teams**

#### **How to Use This Guide as a Client**

If you're a client receiving an AI SOW, use this guide to evaluate vendor proposals:

#### **Red Flags to Watch For**

❌ **Vague Metrics**:
- "95% accuracy" without defining what's measured
- "High quality" without rubric
- "Enterprise-grade" without SLAs

❌ **Missing Evaluation Plan**:
- No test dataset defined
- No measurement methodology
- No acceptance criteria
- Subjective "client satisfaction" as success measure

❌ **Undefined Scope Boundaries**:
- No out-of-scope section
- Ambiguous deliverables ("chatbot with personas")
- No change control process

❌ **Missing Artifacts**:
- No evaluation dataset to be delivered
- No documentation commitments
- No observability plan

❌ **Unrealistic Promises**:
- "100% accuracy" on open-ended tasks
- "Zero hallucinations" without caveats
- Timelines much faster than industry standard

#### **Questions to Ask Vendors**

1. **About Metrics**:
   - "How exactly will you measure this metric?"
   - "On what dataset?"
   - "How will we validate the measurement?"
   - "What's the baseline we're improving from?"

2. **About Evaluation**:
   - "When will we create the test dataset?"
   - "Who validates the test data?"
   - "How do we know the test is representative?"
   - "Can we see the evaluation process?"

3. **About Scope**:
   - "What exactly is NOT included?"
   - "What happens if we want to add X?"
   - "What are our responsibilities?"
   - "What could cause delays?"

4. **About Risk**:
   - "What are the technical risks?"
   - "What could prevent success?"
   - "What assumptions are you making?"
   - "What happens if metrics aren't met?"

#### **Your Responsibilities as Client**

To ensure project success, clients must:

1. **Participate in Definition Workshop**:
   - Allocate time for scoping sessions
   - Bring subject matter experts
   - Provide honest feedback
   - Make decisions on trade-offs

2. **Provide Data and Context**:
   - Share representative data early
   - Define data sources clearly
   - Explain business context
   - Identify edge cases

3. **Create/Validate Test Datasets**:
   - Allocate SME time for annotation
   - Provide ground truth labels
   - Review test scenarios
   - Sign off on evaluation plan

4. **Make Timely Decisions**:
   - Review deliverables promptly
   - Provide feedback within agreed windows
   - Approve changes or raise concerns quickly
   - Don't introduce new requirements late

5. **Prepare for Acceptance**:
   - Allocate time for acceptance testing
   - Assemble evaluation team
   - Review acceptance criteria beforehand
   - Be ready to sign off or articulate concerns

---

## **12. Quick Reference Materials**

### **12.1 One-Page SOW Checklist (Printable)**

```
□ DELIVERABLE DEFINITION
  □ Named & typed (capability/asset/stage)
  □ Uses template from Section 5
  □ S.M.A.R.T.A.I. criteria met
  □ Business value stated

□ DATA & SOURCES
  □ All data sources enumerated & frozen
  □ Data access confirmed
  □ Freshness policy defined
  □ Privacy/security requirements clear

□ MODEL & TECHNOLOGY
  □ Model/provider specified (name + version)
  □ All parameters documented
  □ Infrastructure defined
  □ Fallback plan stated

□ EVALUATION
  □ Test dataset named, sized, versioned
  □ Sampling method defined
  □ Dataset ownership clear
  □ Rubric documented with examples
  □ IAA target set (if human annotation)
  □ LLM-judge calibrated (if applicable)

□ METRICS & THRESHOLDS
  □ All metrics from Section 6 catalog
  □ Thresholds set for each metric
  □ Measurement method defined
  □ Baseline documented (if improving existing)
  □ Performance budgets (latency, cost)

□ ACCEPTANCE CRITERIA
  □ Binary pass/fail criteria only
  □ Single frozen run process defined
  □ Logging/observability specified
  □ Report format agreed
  □ Sign-off owner identified

□ OBSERVABILITY
  □ Monitoring platform specified
  □ Dashboard requirements defined
  □ Alert thresholds set
  □ Logging scope defined

□ SAFETY & SECURITY
  □ Guardrails defined
  □ PII handling specified
  □ Compliance requirements listed
  □ Security assessment planned

□ OUT-OF-SCOPE
  □ Explicit exclusions listed
  □ Change triggers defined
  □ Change control process documented

□ ARTIFACTS
  □ Code deliverables listed
  □ Documentation requirements specified
  □ Dataset deliverables listed
  □ Dashboard/observability deliverables

□ TIMELINE
  □ Milestones with dates
  □ Dependencies identified
  □ Review/approval points scheduled
  □ Acceptance timeline defined

□ APPENDICES (All Mandatory)
  □ Glossary of Terms
  □ Evaluation Rubrics
  □ Test Dataset Specifications
  □ Example Interactions (if applicable)
  □ Integration Specifications (if applicable)
  □ Success Criteria Summary
  □ Architecture Diagrams
  □ RACI Matrix

□ GOVERNANCE
  □ RACI defined
  □ Communication plan
  □ Escalation process
  □ Risk register

□ FINAL REVIEW
  □ Gate 1 (Pre-SOW) approval obtained
  □ Client workshop completed
  □ Internal technical review passed
  □ Legal review completed (if required)
  □ Pricing approved
  □ Client signature obtained
```

---

### **12.2 Deliverable Definition Block (Copy/Paste Template)**

```markdown
## Deliverable: [Name]

**Type**: [Capability / Asset / Stage]
**Stage**: [PoC / Pilot / Production]
**Owner(s)**: [Client role]
**Version**: [e.g., 1.0]

### Objective
[What business problem does this solve?]

### Scope
**In Scope**:
- [Item 1]
- [Item 2]

**Out of Scope**:
- [Item 1]
- [Item 2]

### Technical Specification
**Environment(s)**: [Dev / Pre-Prod / Production]
**Data Sources (frozen)**: [List with versions]
**Model & Parameters**: [Provider, model, temperature, top_p, etc.]
**Infrastructure**: [Cloud provider, region, compute]

### Evaluation
**Evaluation Dataset**:
- Name: [e.g., EvalSet v1.2]
- Size: [n=X]
- Composition: [Describe]
- Source: [Origin]

**Metrics & Thresholds**:
| Metric | Threshold | Method |
|--------|-----------|--------|
| [Metric 1] | ≥/≤ [value] | [Method] |
| [Metric 2] | ≥/≤ [value] | [Method] |

### Acceptance Criteria
[Binary pass/fail criteria - see Section 6]

### Performance Requirements
- **P95 Latency**: ≤ [X] seconds
- **Cost/Query**: ≤ $[X]
- **Throughput**: [X] queries/second

### Security & Compliance
- Data Residency: [Region]
- PII Handling: [Policy]
- Access Control: [RBAC definition]
- Compliance: [Standards, e.g., SOC 2]

### Observability
- Platform: [e.g., Langfuse, Azure AI Foundry]
- Dashboard: [Link or description]
- Alerts: [Threshold definitions]

### Artifacts Delivered
- [ ] [Artifact 1]
- [ ] [Artifact 2]
- [ ] Architecture diagram
- [ ] Evaluation dataset
- [ ] Acceptance report
- [ ] Documentation (user, admin, API)

### Timeline
- Design Review: [Date]
- Development Complete: [Date]
- Testing Complete: [Date]
- Acceptance Run: [Date]
- Production Deployment: [Date]

### Sign-off
**Client Product Owner**: _________________ **Date**: _______
**Vendor Tech Lead**: _________________ **Date**: _______
**Project Manager**: _________________ **Date**: _______
```

---

### **12.3 Metric Quick Reference (Common Targets)**

| Use Case | Key Metrics | Typical Targets |
|----------|-------------|-----------------|
| **RAG QA** | Recall@K, Faithfulness, Latency | ≥0.85, ≥0.90, ≤2.5s |
| **Chatbot** | TSR, FCR, Containment | ≥0.80, ≥0.70, ≥0.75 |
| **Agent Workflow** | Plan Completion, Task Success | ≥0.85, ≥0.80 |
| **Classification** | Macro F1, Per-class Recall | ≥0.85, ≥0.90 (critical) |
| **Extraction** | EM per field, F1 per field | ≥0.80, ≥0.85 |
| **Summarization** | Faithfulness, Coverage, Coherence | ≥0.90, ≥0.85, ≥4.0/5 |

---

### **12.4 Ready-Made Contract Language**

Use these clauses in legal agreements:

#### **Acceptance Clause**
> "Acceptance shall be determined by a single frozen evaluation run executed in the pre-production environment on the named dataset version (EvalSet v[X.Y]) with the specified model, parameters, and configuration as documented in Appendix [X]. Acceptance criteria are the metric thresholds stated in Section [X] of this SOW. All metric thresholds must be met or exceeded for acceptance to be granted. Any modification to data sources, dataset versions, model/provider, thresholds, parameters, or evaluation environments will be handled via a mutually agreed change order as defined in Section [X]."

#### **Deliverable Artifacts Clause**
> "The Contractor shall deliver all evaluation artifacts sufficient to reproduce the acceptance run, including: (i) dataset manifests with version identifiers, (ii) evaluation rubric documentation with annotated examples, (iii) complete prompt library with version history, (iv) evaluation harness source code, (v) configuration files specifying all parameters, (vi) metric computation methodology, (vii) complete evaluation run logs, and (viii) acceptance test report with visualizations. These artifacts shall be delivered within [30] days of acceptance and stored in the agreed repository location as specified in Appendix [X]."

#### **Change Control Clause**
> "Any changes to the following constitute a material change to scope and require a formal change order with mutual written agreement: (i) data sources or data schema, (ii) evaluation dataset version or composition, (iii) model provider, model version, or inference parameters, (iv) acceptance metric definitions or threshold values, (v) performance requirements (latency, cost, throughput), (vi) security or compliance requirements, (vii) integration specifications or API contracts, (viii) deliverable artifacts or documentation requirements, or (ix) project timeline or milestones. Change orders will document impact to scope, schedule, cost, and risk, and require approval from [designated authorities] before implementation."

#### **Client Responsibilities Clause**
> "The Client shall: (i) provide representative data samples and access to data sources within [X] business days of contract execution, (ii) designate subject matter experts to participate in evaluation dataset creation and validation within [X] weeks, (iii) review and approve evaluation rubrics and acceptance criteria within [X] business days of submission, (iv) provide timely feedback on deliverable reviews within [X] business days, (v) make available necessary system access and API credentials for integrations, (vi) participate in scheduled definition workshops and design reviews, and (vii) provide final acceptance sign-off within [X] business days of satisfactory completion of the acceptance run. Delays in Client responsibilities may result in project timeline adjustments as documented through the change control process."

---

## **Conclusion**

### **The Transformation**

By adopting these practices, your organization will transform from:

**FROM**:
- ❌ "We'll build a RAG system with 95% accuracy"
- ❌ Scope disputes and endless iterations
- ❌ Subjective acceptance criteria
- ❌ "Almost done" projects that never close
- ❌ Frustrated teams and unhappy clients

**TO**:
- ✅ "We'll deliver a RAG QA system achieving Recall@8 ≥0.85, MRR ≥0.60, and Faithfulness ≥0.90 on EvalSet v1.2, measured via a single frozen acceptance run"
- ✅ Clear boundaries and predictable scope
- ✅ Binary pass/fail acceptance criteria
- ✅ Projects that close on time with client satisfaction
- ✅ Productive teams and delighted clients

### **The Competitive Advantage**

Organizations that implement these practices gain:

1. **Client Trust**: Demonstrate maturity and reliability
2. **Predictable Delivery**: Reduce variance in project outcomes
3. **Faster Closeout**: Eliminate acceptance ambiguity
4. **Higher Margins**: Fewer surprises, less rework
5. **Reusable IP**: Templated approaches accelerate future projects
6. **Market Differentiation**: Stand out as the disciplined AI partner

### **Getting Started**

**Week 1**: 
- Train sales team on S.M.A.R.T.A.I. framework
- Share example rewrites (Section 8)
- Schedule first definition workshop

**Week 2-4**:
- Apply templates to active opportunities
- Conduct Gate 1 reviews on draft SOWs
- Build internal metrics library

**Month 2**:
- Review first projects using new framework
- Capture lessons learned
- Refine templates based on experience

**Month 3+**:
- Make this framework mandatory for all GenAI SOWs
- Build knowledge base of reusable specifications
- Measure impact on project success metrics

### **Final Thought**

> **The time invested in defining precise, measurable deliverables pays exponential dividends throughout the project lifecycle. Ambiguity is risk. Clarity is value.**

Every successful GenAI project starts with a clear, unambiguous answer to: **"How will we know when this is done?"**

This guide provides the tools, templates, and processes to answer that question with confidence—every single time.

---

**Document Version**: 2.0  
**Last Updated**: October 2025  
**Maintained By**: Solutions Architecture & AI Practice Leadership  
**Next Review**: January 2026

---

**Appendix I: Document History**

| Version | Date | Changes | Author |
|---------|------|---------|--------|
| 1.0 | [Date] | Initial compilation from source documents | [Name] |
| 2.0 | October 2025 | Comprehensive consolidation and standardization | [Name] |

---

*For questions, clarifications, or suggestions for improvement, contact: [AI Practice Leadership]*

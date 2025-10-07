# Best Practices for Creating Non-Ambiguous Deliverables in Generative AI Projects

## Executive Summary

Ambiguous deliverables in Statements of Work (SOWs) are the leading cause of scope disputes, project overruns, and client dissatisfaction in generative AI projects. Terms like "95% accuracy," "chatbot with personas," or "agentic use cases" mean different things to different stakeholders and lead to misaligned expectations.

This document provides frameworks and templates to ensure every deliverable in a Gen AI project is:
- **Measurable**: Clear success criteria with specific metrics
- **Testable**: Defined evaluation methodology
- **Scoped**: Boundaries explicitly stated
- **Unambiguous**: No room for interpretation differences

## Why This Matters: Business Impact

**Without Clear Deliverables:**
- Projects extend 30-50% beyond planned timelines due to scope clarification
- Client disputes arise over whether deliverables are "complete"
- Engineering teams waste time building features not actually required
- Revenue recognition is delayed due to acceptance criteria disputes
- Client satisfaction scores drop, damaging repeat business

**With Clear Deliverables:**
- Reduced change orders and scope creep
- Faster client sign-off and project closure
- Improved team morale and efficiency
- Higher client satisfaction and reference-ability

---

## Core Principles for Writing Clear Deliverables

### 1. **The "Stranger Test"**
Could a stranger with technical knowledge understand exactly what you're committing to deliver? If not, it's too ambiguous.

### 2. **Define Success Criteria First**
Never write a deliverable without simultaneously defining how it will be evaluated and accepted.

### 3. **Quantify Everything Possible**
Replace qualitative terms with specific numbers, percentages, or measurable behaviors.

### 4. **State What's Excluded**
Ambiguity often hides in what's NOT said. Explicitly state scope boundaries.

### 5. **Use Standard Definitions**
Maintain a glossary of terms used consistently across all SOWs in your organization.

---

## Common Ambiguous Deliverables and How to Fix Them

### ❌ BAD: "RAG search with 95% accuracy"

**Problems:**
- What is being measured? Retrieval accuracy? Answer accuracy?
- How is accuracy calculated? Top-1? Top-5? Mean Reciprocal Rank?
- On what data? What types of queries?
- Who determines if it passes?

### ✅ GOOD: "RAG-based Question Answering System"

**Deliverable Specifications:**

**Functional Requirements:**
- System accepts natural language questions via API endpoint
- Returns answers with source citations from provided document corpus
- Maximum response time: 5 seconds (95th percentile)
- Supports document corpus of up to 10,000 documents (500 pages average)
- Document formats: PDF, DOCX, TXT, HTML

**Performance Metrics:**
1. **Answer Relevance**: Average score ≥ 4.0/5.0 on human evaluation rubric (Appendix A) across 100-question test set
2. **Source Attribution Accuracy**: ≥ 90% of answers must cite a relevant source passage (as verified by human evaluators)
3. **Retrieval Quality**: Top-5 retrieved chunks must contain answer-relevant information for ≥ 85% of test queries (measured via annotation protocol in Appendix B)

**Evaluation Methodology:**
- Client provides 100 representative questions with ground truth answers during requirements phase
- System performance measured against this test set before acceptance
- Human evaluation performed by panel of 3 client subject matter experts using standardized rubric
- Acceptance requires meeting all three thresholds above

**Explicitly Out of Scope:**
- Multi-turn conversational memory
- Questions requiring information synthesis across >5 documents
- Real-time document updates (batch processing only)
- Languages other than English

---

### ❌ BAD: "Chatbot with 2 personas"

**Problems:**
- What defines a "persona"? Tone of voice? Domain expertise? Response style?
- How are personas triggered or selected?
- What specific behaviors distinguish the personas?
- How is persona consistency measured?

### ✅ GOOD: "Multi-Persona Customer Service Chatbot"

**Deliverable Specifications:**

**Persona Definitions:**

**Persona 1: Technical Support Agent**
- **Purpose**: Handles troubleshooting, technical questions, error resolution
- **Tone**: Professional, precise, uses technical terminology appropriately
- **Behavior**: Asks clarifying questions, provides step-by-step instructions, requests diagnostic information
- **Trigger**: Automatically activated when user query contains technical keywords (list in Appendix C) or user explicitly requests technical help
- **Example interactions**: See Appendix D

**Persona 2: Sales Advisor**
- **Purpose**: Assists with product selection, feature comparisons, purchase decisions
- **Tone**: Friendly, consultative, persuasive but not pushy
- **Behavior**: Asks about use cases, recommends products, highlights benefits, can explain pricing
- **Trigger**: Automatically activated when user query contains shopping intent keywords or user explicitly requests purchase assistance
- **Example interactions**: See Appendix E

**Persona Switching:**
- System automatically detects and switches personas based on user intent (classification accuracy ≥ 85% on test set)
- User can explicitly request persona switch with commands like "I need technical help" or "Help me buy"
- System announces persona switch in conversation: "Switching you to our technical support specialist..."

**Acceptance Criteria:**
1. Persona classification accuracy ≥ 85% on 200-utterance labeled test set (provided by client)
2. Human evaluators rate persona consistency at ≥ 4/5 across 50 multi-turn conversations (10+ turns each)
3. Zero instances of persona mixing within single response (evaluated on 100 responses)
4. Successful persona switching within 1 conversational turn of trigger event (95% of cases)

**Out of Scope:**
- More than 2 personas
- Persona customization by end users
- Real-time persona training or adjustment
- Emotional tone detection beyond intent classification

---

### ❌ BAD: "Will build 3 agentic use cases"

**Problems:**
- What defines a "use case"? A button? A workflow? A complete application?
- What makes something "agentic" vs. standard automation?
- What level of complexity is expected per use case?
- How is completion determined?

### ✅ GOOD: "Three AI Agent Workflows for Business Process Automation"

**Deliverable Specifications:**

For EACH workflow, the following will be delivered:

**1. Workflow Definition Document** including:
- Process flow diagram showing decision points and agent actions
- Input/output specifications
- Success/failure conditions
- Error handling procedures
- Human-in-the-loop escalation triggers

**2. Implemented Agent** with:
- Autonomous execution capability (runs without human intervention for defined happy path)
- Multi-step reasoning demonstrated through chain-of-thought logging
- Tool/API integration as required by workflow (maximum 5 external integrations per agent)
- Error recovery: Automatic retry logic with exponential backoff
- Human escalation: Handoff to human operator when confidence < 70% or after 3 failed attempts

**3. Agent Capabilities per Use Case:**
- **Minimum**: 3 decision points, 5 distinct actions, 2 external system integrations
- **Execution time**: Completes workflow in < 10 minutes (95th percentile)
- **Reliability**: Successfully completes workflow ≥ 80% of the time on test scenarios without human intervention

**Agreed-Upon Use Cases** (finalized during discovery phase):

**Use Case 1: Invoice Processing Agent**
- Receives invoice emails, extracts data, validates against PO system, routes for approval, updates accounting system
- Decision points: PO match validation, amount threshold check, vendor verification
- Integrations: Email system, PO database, accounting software API

**Use Case 2: Customer Onboarding Agent**
- Guides new customer through account setup, collects required documentation, validates information, provisions access
- Decision points: Documentation completeness, identity verification, account tier selection
- Integrations: CRM, identity verification service, provisioning system

**Use Case 3: IT Helpdesk Ticket Triage Agent**
- Analyzes incoming support tickets, categorizes by issue type, assigns priority, routes to appropriate team, auto-resolves simple cases
- Decision points: Issue category classification, priority assessment, auto-resolution eligibility
- Integrations: Ticketing system, knowledge base, team scheduling system

**Acceptance Criteria per Use Case:**
1. Agent completes workflow end-to-end on 80% of test scenarios without human intervention (20 test scenarios per use case provided by client)
2. Decision points demonstrably use reasoning (logged thought process shows consideration of relevant factors)
3. All specified integrations functional and tested
4. Human escalation triggers correctly 100% of the time on designated edge cases
5. Complete documentation delivered per specifications above

**Explicitly Out of Scope:**
- Workflows requiring >5 external integrations
- Real-time learning or model fine-tuning
- Workflows with execution time >30 minutes
- Integration with systems not providing API access
- Additional use cases beyond the three specified

---

## Framework: SMART-T Deliverable Definition

Every deliverable should meet the SMARTAI criteria:

### **S - Specific**
- Exactly what is being delivered?
- What are the components?
- What formats or interfaces?

### **M - Measurable**
- What metrics define success?
- What are the numerical thresholds?
- How will measurement be performed?

### **A - Achievable**
- Is this technically feasible with current Gen AI capabilities?
- Are the required resources available?
- Are timelines realistic?

### **R - Relevant**
- Does this deliverable align with client's stated business objectives?
- Will it integrate with their existing systems?
- Does it solve the actual problem?

### **T - Time-bound**
- What is the delivery date?
- What are intermediate milestones?
- When will acceptance testing occur?

### **A - Auditable**
- What is the test data?
- How are evaluations being conducted?
- How are logs kept and delivered?

### **A - Interpretable**
- Are the outputs explainable?
- Is there a form of tracability?
- What is the form of confidence scoring?

| Attribute         | Description                                                                     | Example                                                                                    |
| ----------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Specific**      | Define precisely what will be built and what it will do.                        | “RAG chatbot for internal policy documents with conversational retrieval over 10k PDFs.”   |
| **Measurable**    | Quantify performance through defined metrics and evaluation sets.               | “≥85% factual accuracy on 500 QA pairs measured via RAGAS Factuality.”                     |
| **Achievable**    | Ensure deliverables fit time, data, and budget constraints.                     | “Fine-tuning 10k samples using Azure OpenAI GPT-4-Turbo within 8-week delivery.”           |
| **Relevant**      | Tie outcomes to measurable business impact.                                     | “Reduces manual RFP response drafting time by 40%.”                                        |
| **Time-Bound**    | Set delivery windows and validation checkpoints.                                | “Phase 1: prototype in 3 weeks; Phase 2: production in 6 weeks.”                           |
| **Auditable**     | Deliverables must include test data, evaluation reports, and traceability logs. | “All runs logged in Langfuse; eval results stored in Azure Blob and shared via dashboard.” |
| **Interpretable** | Model outputs must be explainable with traceability and confidence scoring.     | “RAG includes citation links and confidence scores per response.”                          |


---

## Category-Specific Guidelines

### Accuracy and Performance Metrics

**Never use standalone accuracy claims.** Always specify:

#### For Classification/Categorization Tasks:
```
Metric: F1 Score (macro-averaged)
Threshold: ≥ 0.85
Dataset: 1,000 labeled examples provided by client during requirements phase
Classes: [List specific categories]
Evaluation: Stratified random split (80/20 train/test), client validates test set labels
```

#### For Information Retrieval:
```
Metric: Mean Reciprocal Rank (MRR) at k=5
Threshold: ≥ 0.75
Dataset: 200 query-document relevance judgments (client-provided or jointly created)
Relevance Definition: Document contains information sufficient to answer query (binary)
Evaluation: Independent test set, 2 annotators with conflict resolution
```

#### For Generation Quality:
```
Metric: Human preference score (comparative A/B testing against baseline)
Threshold: System preferred ≥ 65% of the time
Dataset: 100 representative prompts/scenarios
Evaluators: Panel of 5 client SMEs using blind evaluation
Rubric: See Appendix [X] (includes factual accuracy, relevance, coherence, safety)
```

#### For Response Time:
```
Metric: 95th percentile latency
Threshold: ≤ 5 seconds
Load: Measured at 10 concurrent users
Infrastructure: [Specify environment: cloud region, instance types, etc.]
Measurement: Averaged over 1,000 requests
```

### Model and Technology Specifications

**Always specify:**

#### Model Details:
```
Base Model: GPT-4 Turbo (or equivalent capability, client-approved)
Context Window: 128K tokens
Temperature: 0.7 (configurable by client post-delivery)
Fallback: If primary model unavailable, system uses [backup model] with notification
```

#### Fine-tuning (if applicable):
```
Training Data: Minimum 500 client-provided examples
Validation: 20% held-out set, performance thresholds [specify]
Deliverable: Fine-tuned model checkpoint + training metrics report
Retraining: Included/Not included in scope [specify]
```

#### Infrastructure:
```
Hosting: [AWS/Azure/GCP] in [region]
Availability: 99.5% uptime (measured monthly, excluding planned maintenance)
Scalability: Supports up to [X] concurrent users / [Y] requests per second
Disaster Recovery: [Specify RTO/RPO if applicable]
```

### Integration Deliverables

```
API Specifications:
- Protocol: REST API with OpenAPI 3.0 specification
- Authentication: OAuth 2.0 / API key [specify]
- Endpoints: [List with methods and descriptions]
- Rate Limits: [X] requests per minute per API key
- Response Format: JSON with schema defined in Appendix [X]
- Error Handling: HTTP status codes with descriptive messages (documented)

Documentation Deliverables:
- API reference documentation (hosted on [platform])
- Integration guide with code examples in [languages]
- Postman collection / SDK in [languages: specify]

Testing:
- Client completes successful integration in staging environment
- [X] end-to-end test scenarios executed successfully
```

### Data Deliverables

**Never assume.** Always specify:

```
Training/Fine-tuning Data:
- Client provides: [Specify format, quantity, timeline]
- Vendor provides: [If applicable, specify sources and licensing]
- Data quality requirements: [Completeness, accuracy, recency thresholds]

Data Processing:
- Delivered: Preprocessing pipeline code and documentation
- Format: [Input formats → Output formats]
- Validation: Data quality report showing [specific metrics]

Ongoing Data:
- Updates: Scheduled retraining [frequency] / Ad-hoc [process]
- Client responsibilities: Provide [X] new labeled examples per [timeframe]
- Vendor responsibilities: [Specify if any]
```

---

## Mandatory SOW Appendices

Every Gen AI SOW must include these appendices to eliminate ambiguity:

### Appendix A: Evaluation Rubrics
- Detailed scoring criteria for any human evaluation metrics
- Scale definitions (e.g., what "4/5" means specifically)
- Example scored responses

### Appendix B: Test Datasets
- Source and composition of test data
- Process for creating/validating test sets
- Who owns test data creation
- Timeline for test data delivery

### Appendix C: Glossary of Terms
- Project-specific definitions of ambiguous terms
- Technical definitions agreed upon by both parties

### Appendix D: Example Interactions
- Representative examples of expected system behavior
- Edge cases and how they should be handled
- Non-examples (what the system should NOT do)

### Appendix E: Integration Specifications
- Detailed technical specifications for any integrations
- API contracts, data schemas
- Authentication and security requirements

### Appendix F: Success Criteria Summary
- One-page checklist of all acceptance criteria
- Sign-off process and timeline
- Stakeholders responsible for approval

---

## SOW Review Checklist

Before finalizing any SOW, ensure every deliverable passes this review:

### ✅ Clarity Check
- [ ] A technical person unfamiliar with the project could understand exactly what's being delivered
- [ ] No subjective terms like "high quality," "robust," "intelligent" without definitions
- [ ] All technical terms defined in glossary
- [ ] Specific numbers/thresholds included where applicable

### ✅ Measurement Check
- [ ] Every performance claim has defined measurement methodology
- [ ] Test datasets are specified (size, source, creation process)
- [ ] Evaluation process is detailed (who, when, how)
- [ ] Acceptance criteria are binary (pass/fail, no judgment calls)

### ✅ Scope Check
- [ ] Included features/capabilities explicitly listed
- [ ] Excluded features/capabilities explicitly listed
- [ ] Integration boundaries defined (what systems, what data flows)
- [ ] Scalability limits stated (users, volume, complexity)

### ✅ Accountability Check
- [ ] Client responsibilities clearly stated
- [ ] Vendor responsibilities clearly stated
- [ ] Dependencies identified with mitigation plans
- [ ] Timeline includes client approval/feedback windows

### ✅ Risk Mitigation Check
- [ ] Assumptions documented
- [ ] Contingency plans for common Gen AI challenges (e.g., model availability, API changes)
- [ ] Change request process defined
- [ ] Dispute resolution process defined

---

## Common Pitfalls and How to Avoid Them

### Pitfall 1: "The Demo Trap"
**Problem**: Client sees impressive demo, assumes production system will work the same way on their data.

**Solution**: 
- Always specify demo conditions explicitly: "Demo shown on curated dataset of 50 examples"
- Include in SOW: "Production performance measured on client's actual data, which may differ from demo performance"
- Set realistic expectations about edge cases and failure modes

### Pitfall 2: "Accuracy Theater"
**Problem**: Claiming "95% accuracy" sounds good but is meaningless without context.

**Solution**:
- Always use multiple metrics (precision, recall, F1, not just accuracy)
- Always specify the difficulty of the test set
- Always compare to baseline (human performance, random baseline, existing system)
- Example: "F1 score ≥ 0.85, which represents 40% improvement over client's current rule-based system (F1 = 0.60)"

### Pitfall 3: "Feature Creep via Vagueness"
**Problem**: Terms like "chatbot" can encompass infinite features.

**Solution**:
- List specific capabilities included
- List specific capabilities NOT included
- Define upgrade path for additional features (separate SOW/change order)

### Pitfall 4: "The Subjective Acceptance"
**Problem**: "Client must be satisfied with the quality" is not testable.

**Solution**:
- Replace subjective acceptance with objective criteria
- If subjective evaluation necessary, use structured methodology (defined rubrics, multiple evaluators, statistical criteria)
- Include dispute resolution: "If acceptance criteria met but client disagrees on quality, third-party evaluation will be performed using [specified rubric]"

### Pitfall 5: "Implied Capabilities"
**Problem**: Client assumes capabilities common in consumer AI tools (like ChatGPT) will be in the deliverable.

**Solution**:
- Don't assume client understands technical limitations
- Explicitly state what system CANNOT do
- Provide reference examples of in-scope vs. out-of-scope queries/tasks

---

## Template: Deliverable Specification Sheet

Use this template for each major deliverable:

```markdown
## Deliverable: [Name]

### Description
[2-3 sentence plain-language description of what this is]

### Functional Requirements
- [Specific capability 1]
- [Specific capability 2]
- [Specific capability 3]
[Continue as needed]

### Performance Requirements
| Metric | Threshold | Measurement Method |
|--------|-----------|-------------------|
| [Metric 1] | ≥ / ≤ [number] | [How measured] |
| [Metric 2] | ≥ / ≤ [number] | [How measured] |

### Technical Specifications
- **Model/Technology**: [Specific model or technology stack]
- **Infrastructure**: [Hosting, scaling, availability requirements]
- **Integrations**: [List systems and integration methods]
- **Data Requirements**: [Input/output formats, volume, update frequency]

### Acceptance Criteria
1. [Specific, testable criterion 1]
2. [Specific, testable criterion 2]
3. [Specific, testable criterion 3]
[All must be pass/fail, no subjective evaluation]

### Testing Methodology
- **Test Dataset**: [Source, size, composition]
- **Evaluation Process**: [Who tests, how, when]
- **Success Threshold**: [Clear pass/fail criteria]

### Dependencies
- **Client Provides**: [Data, access, resources, decisions]
- **Vendor Requires**: [Third-party services, approvals, infrastructure]

### Explicitly Out of Scope
- [Capability or feature NOT included]
- [Capability or feature NOT included]
- [Capability or feature NOT included]

### Delivery Timeline
- **Milestone 1**: [Deliverable component] by [Date]
- **Milestone 2**: [Deliverable component] by [Date]
- **Final Delivery**: [Date]
- **Acceptance Testing**: [Date range]

### Documentation Included
- [ ] Technical architecture document
- [ ] User guide / API documentation
- [ ] Testing report
- [ ] [Other documentation]
```

---

## Implementation Recommendations

### For Sales Teams:
1. **Conduct technical scoping calls** before finalizing SOW - include solutions architects
2. **Use this document's templates** as standard operating procedure
3. **Get client sign-off on test datasets** during requirements phase, not at delivery
4. **Budget time for specification** - rushing SOW creation causes project problems
5. **When in doubt, be more specific** - over-specification is better than ambiguity

### For Project Management:
1. **Reference SOW specifications in all status updates** - keep everyone aligned on what "done" means
2. **Flag scope creep early** - if client requests something not in SOW, initiate change order process immediately
3. **Document assumptions** - if something is ambiguous, document your interpretation and get client confirmation

### For Engineering Teams:
1. **Challenge vague requirements before starting work** - push back to sales/PM if deliverable is ambiguous
2. **Propose measurement methodologies early** - don't wait until delivery to figure out how success is measured
3. **Document limitations honestly** - if you know something won't work in production like it did in demo, communicate early

---

## Conclusion

Clear, unambiguous deliverables are the foundation of successful generative AI projects. They:
- Align expectations between sales, engineering, and clients
- Prevent scope creep and disputes
- Enable objective acceptance criteria
- Improve project velocity and client satisfaction

The additional time invested in creating precise deliverable specifications in the SOW pays dividends throughout the project lifecycle and dramatically reduces risk.

**Key Takeaway**: If you can't measure it objectively, you can't deliver it reliably. Every deliverable must answer: "How will we know when this is done?"

---

## Appendix: Quick Reference - Red Flags in Deliverables

| ❌ Red Flag | ✅ Fix |
|-------------|--------|
| "High accuracy" | "F1 score ≥ 0.85 on 1,000-example client test set" |
| "Intelligent routing" | "Classifies into 5 categories with ≥ 90% precision, evaluated on 500-ticket test set" |
| "Natural conversations" | "Handles 10+ turn conversations maintaining context, evaluated on 50 test dialogues with ≥ 4/5 coherence rating" |
| "Real-time processing" | "95th percentile latency ≤ 2 seconds under 50 concurrent user load" |
| "Comprehensive documentation" | "API reference, integration guide with 5 code examples, troubleshooting guide - totaling minimum 25 pages" |
| "Enterprise-grade" | "99.5% uptime, SOC 2 compliant infrastructure, supports 1000 concurrent users, 24/7 monitoring" |
| "Agentic workflow" | "Autonomous execution through 7 defined steps with 4 decision points, 80% completion rate without human intervention on test scenarios" |
| "Custom AI model" | "Fine-tuned GPT-4 Turbo on 1,000 client examples, with ≥ 20% performance improvement over base model on held-out test set" |

---

*Document Version: 1.0*  
*Last Updated: [Date]*  
*Owner: [Solutions Architecture / Sales Engineering Team]*

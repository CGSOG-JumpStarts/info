

## **A Practical Guide to Scoping Generative AI Projects: The Clarity Framework**

### **1. Introduction: The Strategic Imperative for Clarity**

Generative AI projects are not traditional software development. They are inherently probabilistic, dependent on data quality, and often exploratory in nature. Vague statements in a Statement of Work (SOW) such as "build a RAG system with 95% accuracy" or "create 3 agentic use cases" are not just imprecise; they are a direct path to scope creep, client dissatisfaction, and project failure.

This document establishes a framework for creating non-ambiguous, measurable, and mutually understood deliverables for Generative AI projects. Its purpose is to equip sales, solutioning, and delivery teams with a shared language to define success, manage client expectations, and ensure profitable, successful engagements. By moving from ambiguity to clarity, we position ourselves as a mature, reliable, and strategic AI partner.

### **2. Guiding Principles**

1.  **Define Everything, Assume Nothing:** Every technical term, metric, and concept must be explicitly defined in the SOW.
2.  **Focus on Measurable Outcomes:** Shift from listing features to defining the observable, quantifiable outcomes the client will receive.
3.  **Embrace Tiered Definitions:** Not all "use cases" or "personas" are created equal. Use a tiered complexity model (e.g., Simple, Moderate, Complex) to align effort with value and cost.
4.  **Co-create Definitions with the Client:** Use definition workshops as a part of the sales process to ensure alignment and build trust. The SOW should document a shared understanding, not impose our own.
5.  **Prioritize Process over Perfection:** Acknowledge that AI performance is iterative. Define the *process and metrics* for evaluation and improvement, not just a static, final number.

### **3. Deliverable Specification Templates**

This section provides a set of standardized templates to define the scope and success criteria for common Generative AI applications. Using these templates is the primary method for eliminating ambiguity in SOWs.

#### **3.1. RAG System Specification Template**

For any project involving Retrieval-Augmented Generation, this template ensures all components are clearly defined, from data sources to the final evaluation metrics.

| Section | Definition & Best Practices |
| :--- | :--- |
| **Objective** | What business problem is the RAG system solving? (e.g., "To allow customer support agents to quickly find answers to technical questions from our internal knowledge base.") |
| **Data Sources** | An exhaustive list of all corpora to be indexed. Be specific about the format and location. (e.g., "Confluence Space 'TechKB'," "SharePoint Document Library 'ProductManuals'," "Public website URL `docs.example.com`.") |
| **Indexing Strategy** | How will the data be processed? <br> **- Chunking Strategy:** (e.g., "Recursive character splitting, 1000-character chunk size, 200-character overlap.") <br> **- Metadata Extraction:** What metadata will be stored with each chunk? (e.g., `source_url`, `document_title`, `last_modified_date`). |
| **Retrieval Strategy**| How will relevant information be found? (e.g., "Vector similarity search using `text-embedding-ada-002`," "Hybrid search combining vector search with keyword-based BM25.") |
| **Generation Model**| Which LLM will be used to synthesize the final answer? (e.g., "OpenAI GPT-4o," "Anthropic Claude 3 Sonnet.") |
| **Evaluation Dataset**| Define the "golden dataset" for testing. (e.g., "A set of 100 question-and-answer pairs, provided and validated by the client's subject matter experts, which will serve as the ground truth for all metrics.") |
| **Evaluation Metrics**| The specific, measurable success criteria. Deconstruct "accuracy" into: <br> **1. Retrieval Relevance:** Measures if the right information was fetched. (e.g., "A **Hit Rate of 90% at K=5** means for 90% of test questions, the correct answer was in the top 5 retrieved documents.") <br> **2. Generation Faithfulness:** Measures if the answer is based only on the retrieved context. (e.g., "A **human-evaluated Faithfulness Score of 4.5/5.0 or higher**.") <br> **3. Answer Correctness:** Measures if the final answer is factually correct. (e.g., "An **Answer Correctness Score of 95%** as determined by client SMEs.") |

#### **3.2. Persona Specification Card Template**

This template is crucial for any conversational AI project. It moves beyond a vague description to a concrete set of behavioral and knowledge-based rules that guide development and testing.

| Attribute | Definition & Best Practices |
| :--- | :--- |
| **Name** | A unique, internal identifier for the persona (e.g., `SupportBot_v1`, `SalesQualifier_Alpha`). This helps in versioning and distinguishing between different bots. |
| **Role** | The persona's primary function in a single, clear sentence. This is the "elevator pitch" for what the bot does. (e.g., "A friendly and professional first-line support agent for product FAQs.") |
| **Knowledge Domain** | Defines the **exact boundaries of the persona's expertise**. List specific data sources (e.g., SharePoint sites, web pages, specific documents). This is critical for preventing scope creep and is the foundation for RAG systems. |
| **Tone of Voice** | A list of adjectives describing the communication style. This directly influences prompt engineering. Examples: `Professional`, `Clear`, `Patient`, `Concise`, `Empathetic`, `Witty`, `Formal`. |
| **Personality Traits**| Specific, observable behaviors. How does it act? (e.g., "Always introduces itself," "Uses 'we' instead of 'I'," "Never speculates or gives opinions," "Uses emojis sparingly.") |
| **Guardrails** | The explicit "do nots." This is a critical safety and compliance component. (e.g., "Will not discuss pricing or contracts," "Will not answer questions outside its knowledge domain," "Will not provide medical or legal advice.") |
| **Escalation Trigger**| The precise conditions under which the persona must hand off to a human agent. (e.g., "User explicitly asks for a human," "User expresses frustration," "The same question is asked 3 times without resolution.") |
| **Key Functions** | A bulleted list of the specific tasks the persona is expected to perform successfully. (e.g., "Answer 'how-to' questions," "Link to specific documentation," "Provide status of known system outages.") |

#### **3.3. Agentic Use Case Specification Sheet Template**

This template is essential for projects involving AI agents that perform tasks. It defines the agent's mission, capabilities, and the criteria for success, turning a vague idea into a testable and deliverable workflow.

| Section | Definition & Best Practices |
| :--- | :--- |
| **Use Case ID** | A unique identifier for tracking and management (e.g., `AGENT-001`). |
| **Mission** | The agent's single, clear objective. What is the ultimate business outcome it needs to achieve? (e.g., "To process inbound email inquiries and draft a response for the correct account owner to review.") |
| **Trigger(s)** | The specific event(s) that initiate the agent's workflow. This defines the starting point. (e.g., "A new email arrives in a specific inbox," "A new record is created in Salesforce," "A user clicks a button in a UI.") |
| **Input(s)** | The data the agent receives or requires to begin its work. Be specific about the data fields (e.g., `Email Subject`, `Email Body`, `Sender's Email Address`). |
| **Tools / Skills** | The **most critical section**. This is a definitive list of the APIs, functions, or other capabilities the agent can use. Each tool should be defined like a function (e.g., `read_email(message_id)`, `search_salesforce_contact(email)`). **If it's not on this list, the agent can't do it.** |
| **Output(s)** | The final, tangible artifact(s) produced by the agent. What does "done" look like? (e.g., "A draft email in the user's Gmail 'Drafts' folder," "A new ticket created in Jira with a summary.") |
| **Success Criteria**| The explicit, binary, and **measurable** conditions that define a successful run. (e.g., "A draft email is created for 99% of inbound inquiries," "The correct account owner is identified in 95% of cases.") |
| **Failure Conditions**| Defines the agent's behavior when it cannot complete its mission. What is the expected fallback? (e.g., "If a contact is not found in Salesforce, the agent will flag the email in the shared inbox and take no further action.") |
| **Complexity Tier** | Categorize the use case to manage scope and pricing: <br> **- Tier 1 (Simple):** Single-step tool use, deterministic. <br> **- Tier 2 (Moderate):** Multi-step, simple conditional logic. <br> **- Tier 3 (Complex):** Requires reasoning, planning, and dynamic tool selection. |

#### **3.4. Content Generation Specification Template**

This template is for projects where the primary deliverable is generated content, such as marketing copy, summaries, or reports.

| Section | Definition & Best Practices |
| :--- | :--- |
| **Content Goal** | What is the purpose of this content? What action should it drive? (e.g., "Generate 5 engaging LinkedIn posts per week to drive traffic to our latest blog article.") |
| **Target Audience** | Who is this content for? Be specific about the audience's role, knowledge level, and motivations. (e.g., "Chief Information Security Officers (CISOs) at mid-sized financial institutions.") |
| **Key Message** | The single most important takeaway the audience should have after reading. (e.g., "Our new security platform reduces compliance risk by automating audit trails.") |
| **Tone & Style** | Define the desired voice. (e.g., "Authoritative yet approachable," "Technical but not academic," "Urgent and action-oriented.") Provide a link to brand style guides if available. |
| **Format & Structure**| Define the output structure. (e.g., "A 500-word blog post with an introduction, 3 main points with sub-bullets, and a concluding call-to-action," "A JSON object with fields: `title`, `summary`, `keywords`.") |
| **Required Inputs** | What source material must the model use? (e.g., "The attached technical whitepaper," "The transcript of the CEO's last keynote speech.") |
| **Constraints & Guardrails** | What should the content *not* include? (e.g., "Do not mention competitors by name," "Avoid making specific pricing promises," "All statistics must be from the last 12 months.") |
| **Quality Metrics** | How will the quality of the generated content be measured? <br> **- Factual Accuracy:** (e.g., "99% of all factual claims must be verifiable against the source material.") <br> **- Brand Alignment:** (e.g., "A score of 4/5 or higher on brand voice alignment, as rated by the marketing team.") <br> **- Engagement Potential:** (e.g., "The content must pass a 'readability' score of grade 10 or lower.") |

### **4. Implementation in the SOW Process**

1.  **Mandatory Definition Annex:** Every GenAI SOW must include a "Definitions & Metrics" annex containing the detailed specifications (RAG, Persona, Agentic, and Content Generation templates) relevant to the project.
2.  **Internal Technical Review:** No GenAI SOW can be sent to a client without a formal review and sign-off from a technical architect. This ensures our promises are deliverable.
3.  **Client Definition Workshop:** Position a 2-4 hour workshop as a standard, non-negotiable part of the final sales cycle. This collaborative session will be used to fill out the specification templates *with the client*, ensuring total alignment before signing. This is a value-add activity that demonstrates our expertise and commitment to their success.

By adopting this Clarity Framework, we will not only mitigate project risk but also elevate our brand. We will be known as the AI partner that brings discipline to innovation, provides transparency in our process, and consistently delivers on our promises.

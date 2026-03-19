
---

# 3) Project plan

## Project title
**Agentic Supply Chain Intelligence: Geopolitical Meta-Risk Impact Mapping**

## Delivery goal
Build an MVP that detects geopolitical events, maps them to commodity and internal supply chain exposure, and produces explainable 1-month and 3-month impact scenarios with validation and observability.

---

## A. Project phases

## Phase 0 — Discovery and scope alignment
**Duration:** 1 week

### Objectives
- confirm business scope
- identify initial commodities
- identify initial regions and routes
- align on alert consumers and KPIs

### Deliverables
- problem statement
- KPI list
- prioritized use cases
- MVP scope document

### Key questions
- Which commodities matter most to the business?
- Which internal plants, suppliers, or materials should be covered first?
- What level of false positives is acceptable?
- What actions should alerts trigger?

---

## Phase 1 — Data backbone
**Duration:** 2 weeks

### Objectives
- ingest external and internal data
- create clean storage structure
- establish enrichment logic

### Workstreams
**1. External data ingestion**
- GDELT events and GKG
- World Bank Pink Sheet
- optional shipping and sanctions reference data

**2. Internal data ingestion**
- supplier master
- material / category mapping
- plant / warehouse dependencies
- procurement spend mapping

**3. Data modeling**
- raw tables
- enriched tables
- exposure mapping tables

### Deliverables
- PySpark ingestion jobs
- schema definitions
- initial warehouse tables
- data quality checks

### Exit criteria
- data jobs run reliably
- at least 6 months to several years of commodity history available
- event records enriched with normalized fields

---

## Phase 2 — Knowledge and retrieval layer
**Duration:** 1 to 2 weeks

### Objectives
- create retrieval and graph foundation for reasoning

### Workstreams
**1. Vector database**
- load historical disruption summaries
- store geopolitical context documents
- create metadata tagging strategy

**2. Knowledge graph**
- define nodes and relationships
- country to port mapping
- port to route mapping
- route to commodity mapping
- commodity to internal material mapping

### Deliverables
- vector index
- graph schema
- graph population scripts
- retrieval interfaces

### Exit criteria
- a query can map event location to commodities
- a query can map commodity to internal exposure
- historical analog documents can be retrieved

---

## Phase 3 — Agentic workflow with LangGraph
**Duration:** 2 weeks

### Objectives
- build orchestration graph
- implement self-correction and verification logic

### Workstreams
**1. State design**
- define workflow state contract
- define agent inputs and outputs

**2. Agent implementation**
- Event Scout
- Verifier
- Commodity Mapper
- Impact Strategist
- Decision Narrator

**3. Conditional routing**
- low-confidence verification
- no-exposure path
- high-severity escalation path
- human review path

### Deliverables
- LangGraph workflow
- prompt templates
- node implementations
- workflow tests

### Exit criteria
- graph runs end to end on sample scenarios
- low-confidence events are re-routed correctly
- output includes structured rationale and citations

---

## Phase 4 — Impact modeling and scenario engine
**Duration:** 1 to 2 weeks

### Objectives
- convert events into business-relevant scenarios

### Workstreams
**1. Event severity scoring**
- event type
- source count
- source diversity
- strategic asset proximity

**2. Commodity exposure scoring**
- export concentration
- route dependence
- supplier concentration
- internal spend impact

**3. Historical sensitivity logic**
- analog event retrieval
- price reaction windows
- lag estimation for 2, 4, 8, 12 weeks

**4. Scenario engine**
- base
- stressed
- severe

### Deliverables
- scoring modules
- scenario engine
- backtesting notebook or script
- structured impact output schema

### Exit criteria
- system can estimate plausible 1-month and 3-month ripple impact
- business output can be explained clearly

---

## Phase 5 — Validation, guardrails, and observability
**Duration:** 1 week

### Objectives
- prove the system is trustworthy
- reduce hallucination risk
- create visibility into agent behavior

### Workstreams
**1. Golden queries**
- create at least 20 high-value test questions

**2. Evaluation**
- Ragas or DeepEval
- faithfulness checks
- tool correctness
- route correctness

**3. Observability**
- trace graph execution
- log tool calls
- capture confidence and alert outcomes

### Deliverables
- eval suite
- regression tests
- dashboards or logs
- pass/fail criteria

### Exit criteria
- golden suite runs automatically
- outputs meet agreed thresholds
- severe alerts are auditable

---

## Phase 6 — API, dashboard, and demo
**Duration:** 1 week

### Objectives
- expose business-facing interface
- prepare demo and stakeholder narrative

### Workstreams
- API endpoint for risk query
- dashboard for active alerts
- executive summary view
- demo storyboards

### Deliverables
- API service
- simple UI
- stakeholder demo deck
- walkthrough scenarios

### Exit criteria
- end users can ask a question and receive grounded response
- demo covers real business scenarios

---

# B. Indicative timeline

## 8-week MVP plan

| Week | Focus | Output |
|---|---|---|
| 1 | Discovery and scope | MVP scope, KPIs, use cases |
| 2 | Data ingestion | GDELT + Pink Sheet pipelines |
| 3 | Knowledge layer | Vector DB + graph schema |
| 4 | LangGraph workflow | Working agent graph |
| 5 | Mapper + strategist | Exposure and scenario logic |
| 6 | Modeling refinement | Historical sensitivity outputs |
| 7 | Validation and observability | Golden tests, faithfulness metrics |
| 8 | API/dashboard/demo | MVP demo and executive walkthrough |

---

# C. Roles and responsibilities

| Role | Responsibility |
|---|---|
| ML Developer | LangGraph workflow, modeling, evaluation |
| Data Engineer | ingestion pipelines, schemas, storage |
| MLOps Engineer | deployment, CI/CD, monitoring, secrets |
| Supply Chain SME | commodity logic, route mapping, validation |
| Procurement / Logistics User | output review, alert usefulness feedback |
| Product Owner | scope, prioritization, stakeholder alignment |

---

# D. MVP success criteria

## Technical success
- ingestion jobs complete successfully on schedule
- workflow executes end to end
- alerts include traceable evidence
- faithfulness score passes defined threshold

## Business success
- users can identify exposure faster than with manual monitoring
- alerts are relevant and actionable
- executives understand timing and magnitude of likely impact
- analysts trust the output enough to use it in decision support

---

# E. Risk register

| Risk | Description | Mitigation |
|---|---|---|
| Noisy news | events may be misleading or duplicated | verifier node, multi-source confirmation |
| Weak causal claims | model may overstate impact | scenario ranges, analog logic, explicit confidence |
| Graph incompleteness | missing mappings reduce usefulness | start with curated high-priority commodities |
| Hallucination | narrative may exceed evidence | faithfulness testing, strict grounding |
| Scope creep | too many regions and commodities at once | tightly scoped MVP |
| User trust | users may reject opaque outputs | citations, confidence, audit logs |

---

# F. Initial golden queries

1. How does a closure of the Suez Canal affect wheat prices?
2. What is the likely 3-month impact of LNG disruption in Qatar?
3. Which commodities are most exposed to Gulf port closures?
4. Which of our suppliers depend on Red Sea transit?
5. What is the likely downstream effect on urea if LNG exports are disrupted?
6. Which internal plants are exposed to ammonia price shocks?
7. Is this event verified strongly enough to trigger a procurement response?
8. What historical events are most similar to this disruption?
9. What is the likely lag before raw material cost impact is observed?
10. What actions should logistics leaders consider in the next 2 weeks?

---

# G. Recommended first demo scenario

Use one scenario only for clarity:

**Scenario:** Gulf export disruption affecting LNG supply  
**Why this works:**  
- easy to explain  
- strong commodity link  
- clear downstream effect into ammonia and urea  
- directly relevant to energy-intensive supply chains

Demo flow:
1. Event appears in GDELT
2. Event Scout identifies it
3. Verifier confirms it
4. Commodity Mapper links it to LNG
5. Impact Strategist links LNG to ammonia / urea ripple risk
6. Decision Narrator generates executive summary
7. Faithfulness score is shown alongside the answer

# agentic-supply-chain-intelligence
An agentic RAG system for supply chain intelligence. Built with langchain, langgraph, GDELT 2.0, and PySpark to map middle east conflict events to global commodity price ripples.



# Agentic Supply Chain Intelligence

## Overview
Agentic Supply Chain Intelligence is a multi-agent system that converts live geopolitical events into explainable supply chain impact scenarios.

The platform is designed to help procurement leaders, logistics teams, and executives answer questions such as:

- What does a port disruption in the Gulf mean for our raw materials?
- Which commodities are likely to be affected over the next 1 to 3 months?
- Which suppliers, plants, or categories are exposed?
- How confident is the system, and what evidence supports the answer?

This project combines:
- real-time geopolitical event monitoring
- retrieval-augmented generation
- knowledge graph reasoning
- historical commodity price analysis
- multi-agent orchestration with LangGraph
- evaluation and guardrails for faithfulness

---

## Business Problem
Traditional dashboards show what is happening now, but they do not reason across:
1. geopolitical events,
2. commodity exposure,
3. route disruption,
4. economic ripple effects,
5. internal supply chain dependency.

This project fills that gap by predicting how verified events may affect supply chain costs and risks over the coming weeks and months.

---

## Objectives
- Detect critical geopolitical events from near-real-time data
- Map event geography to commodities, routes, and internal exposure
- Estimate downstream cost and supply impact
- Generate grounded, explainable executive summaries
- Prevent hallucinations through evaluation and guardrails
- Provide auditable traces for every high-risk alert

---

## Core Use Case
Example:
A disruption near Gulf export infrastructure occurs.

The system should:
1. detect the event,
2. verify it,
3. identify exposed commodities such as LNG or helium,
4. map internal material dependency,
5. estimate likely price ripple in 1 month and 3 months,
6. recommend actions such as alternate sourcing or stock review.

---

## Solution Architecture
The solution has five major parts:

### 1. Data Backbone
- GDELT event and knowledge graph ingestion
- World Bank Pink Sheet commodity price ingestion
- internal master data ingestion
- enrichment and normalization using PySpark

### 2. Retrieval and Knowledge Layer
- vector database for historical context and analyst notes
- knowledge graph for country, port, route, commodity, supplier, and plant dependency

### 3. Multi-Agent Orchestration
Built with LangGraph:
- Event Scout
- Verifier
- Commodity Mapper
- Impact Strategist
- Decision Narrator

### 4. Modeling and Scenario Layer
- event severity scoring
- commodity exposure scoring
- historical analog matching
- scenario generation for near-term and mid-term ripple effects

### 5. Validation and Observability
- golden query test suite
- faithfulness evaluation using Ragas or DeepEval
- agent trace logging
- audit trail for alerts and decisions

---

## Repository Structure

```text
agentic-supply-chain-intel/
├── apps/
│   ├── api/
│   ├── dashboard/
│   └── alert_service/
├── config/
│   ├── settings.yaml
│   ├── prompts.yaml
│   └── logging.yaml
├── data/
│   ├── reference/
│   ├── sample/
│   └── eval/
├── docs/
│   ├── architecture/
│   ├── design_decisions/
│   └── runbooks/
├── jobs/
│   ├── pyspark_ingest_gdelt.py
│   ├── pyspark_ingest_pinksheet.py
│   ├── enrich_events.py
│   ├── build_exposure_graph.py
│   └── generate_training_windows.py
├── graph/
│   ├── state.py
│   ├── workflow.py
│   ├── routing.py
│   ├── nodes/
│   │   ├── event_scout.py
│   │   ├── verifier.py
│   │   ├── commodity_mapper.py
│   │   ├── impact_strategist.py
│   │   └── decision_narrator.py
│   └── prompts/
├── retrieval/
│   ├── vector_store.py
│   ├── graph_queries.py
│   ├── retrievers.py
│   └── rerankers.py
├── models/
│   ├── event_severity.py
│   ├── exposure_scoring.py
│   ├── sensitivity_model.py
│   └── scenario_engine.py
├── serving/
│   ├── schemas.py
│   ├── inference.py
│   └── publisher.py
├── evals/
│   ├── golden_queries.yaml
│   ├── ragas_eval.py
│   ├── deepeval_eval.py
│   └── regression_runner.py
├── observability/
│   ├── tracing.py
│   ├── metrics.py
│   ├── audit_logger.py
│   └── dashboards/
├── tests/
│   ├── unit/
│   ├── integration/
│   ├── graph/
│   └── eval/
├── notebooks/
├── scripts/
├── requirements.txt
├── pyproject.toml
└── README.md

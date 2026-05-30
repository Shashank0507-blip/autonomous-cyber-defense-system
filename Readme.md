# autonomous-cyber-defense-system — Schema-Grounded Cyber Defense System

A multi-agent AI Security Operations Center (SOC) pipeline combining **XGBoost intrusion detection**, **schema-grounded reasoning**, **LLM investigation agents**, and **autonomous remediation orchestration**.

This project simulates an intelligent SOC analyst workflow:

* Detect suspicious traffic using ML.
* Investigate alerts using tool-augmented reasoning.
* Assess severity and threat context.
* Make response decisions.
* Execute remediation actions.
* Generate structured incident reports.

---

# Core Features

### ML Intrusion Detection

Uses an **XGBoost classifier** to predict network attack categories and confidence scores from traffic features.

### Schema-Grounded Security Knowledge Layer

A structured cybersecurity reasoning schema containing:

* Threat intelligence knowledge
* Attack → tool mappings
* Investigation heuristics
* Baseline traffic definitions
* Severity logic
* Function registry

### Investigator Agent

A **ReAct-style reasoning agent** that performs:

Perceive → Reason → Tool Call → Observe loops.

The investigator:

* selects investigation tools
* gathers evidence
* calculates severity
* builds an auditable reasoning trace
* produces investigation summaries

### Decision Agent

Consumes investigator findings and determines:

* BLOCK
* QUARANTINE
* MONITOR
* ALERT
* CLEAR

The decision agent can execute remediation actions and enforce escalation policies.

### Incident Reporting

Generates:

* incident reports
* action logs
* reasoning traces
* human-readable SOC summaries

---

# Architecture

```text
                           ┌──────────────────────────────┐
                           │      ML CLASSIFIER           │
                           │      (XGBoost Model)         │
                           │ attack_label + confidence    │
                           └──────────────┬───────────────┘
                                          │
                                          ▼

┌──────────────────────────────────────────────────────────────────────────┐
│                    CYBERSECURITY KNOWLEDGE SCHEMA                       │
│                                                                          │
│ Structured security reasoning backbone                                  │
│                                                                          │
│ • ATTACK_FUNCTION_MAP                                                    │
│ • THREAT_INTEL                                                           │
│ • FUNCTION_REGISTRY                                                      │
│ • BASELINE traffic behavior                                              │
│ • SOC investigation heuristics                                           │
│ • severity logic                                                         │
└──────────────────────────────┬───────────────────────────────────────────┘
                               │
                               ▼

┌──────────────────────────────────────────────────────────────────────────┐
│                         INVESTIGATOR AGENT                               │
│                                                                          │
│ ReAct reasoning loop                                                     │
│                                                                          │
│ Perceive → Reason → Tool Call → Observe                                 │
│                                                                          │
│ READ-ONLY Investigation Tools                                            │
│                                                                          │
│ • check_port_history()                                                   │
│ • check_flow_rate()                                                      │
│ • check_syn_count()                                                      │
│ • lookup_threat_intel()                                                  │
│ • calculate_severity()                                                   │
│ • get_similar_incidents()                                                │
│                                                                          │
│ Outputs:                                                                 │
│ • reasoning trace                                                        │
│ • severity assessment                                                    │
│ • investigation summary                                                  │
└──────────────────────────────┬───────────────────────────────────────────┘
                               │ investigation_context
                               ▼

┌──────────────────────────────────────────────────────────────────────────┐
│                           DECISION AGENT                                 │
│                                                                          │
│ Determines remediation strategy                                          │
│                                                                          │
│ VERDICTS                                                                  │
│ • BLOCK                                                                   │
│ • QUARANTINE                                                              │
│ • MONITOR                                                                 │
│ • ALERT                                                                   │
│ • CLEAR                                                                   │
│                                                                          │
│ ACTION TOOLS                                                              │
│                                                                          │
│ • log_blocked_ip()                                                        │
│ • quarantine_host()                                                       │
│ • flag_suspicious_ip()                                                    │
│ • alert_admin()                                                           │
│ • log_clear()                                                             │
│                                                                          │
│ Applies:                                                                  │
│ • escalation rules                                                        │
│ • mandatory response logic                                                │
│ • human approval requirements                                             │
└──────────────────────────────┬───────────────────────────────────────────┘
                               │ enriched_context
                               ▼

┌──────────────────────────────────────────────────────────────────────────┐
│                     SYNTHESIS / REPORTING LAYER                          │
│                                                                          │
│ Generates:                                                               │
│                                                                          │
│ • incident reports                                                       │
│ • audit trail                                                            │
│ • SOC analyst summary                                                    │
│ • remediation history                                                    │
│ • structured logs                                                        │
└──────────────────────────────────────────────────────────────────────────┘
```

---

# Project Structure

```text
multi-agent-ai-soc/

├── README.md
├── requirements.txt
├── .gitignore

├── src/

│   ├── classifier/
│   │   ├── train_model.py
│   │   ├── predict.py
│   │   └── saved_model.pkl
│
│   ├── schema/
│   │   ├── threat_intel.py
│   │   ├── attack_mappings.py
│   │   ├── baselines.py
│   │   └── function_registry.py
│
│   ├── agents/
│   │   ├── investigator_agent.py
│   │   ├── decision_agent.py
│   │   └── synthesis_agent.py
│
│   ├── tools/
│   │   ├── investigation_tools.py
│   │   ├── action_tools.py
│   │   └── function_library.py
│
│   └── pipeline/
│       └── orchestrator.py
│
├── reports/
│
├── docs/
│
└── notebooks/
```

---

# Installation

Clone repository:

```bash
git clone <your_repo_url>
cd multi-agent-ai-soc
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Ensure Ollama is running locally.

---

# Usage

Run the orchestration pipeline:

```bash
python src/pipeline/orchestrator.py
```

Run investigator independently:

```bash
python src/agents/investigator_agent.py
```

Run decision agent independently:

```bash
python src/agents/decision_agent.py
```

---

# Example Workflow

```text
Network Traffic
      ↓
XGBoost Prediction
      ↓
Investigator Agent
      ↓
Evidence Gathering
      ↓
Severity Assessment
      ↓
Decision Agent
      ↓
Remediation Actions
      ↓
Incident Report Generation
```

---

# Future Improvements

* Working memory module
* Persistent schema memory
* Threat knowledge graph
* Multi-agent collaboration layer
* Live packet capture integration
* Dashboard visualization
* Human-in-the-loop approval UI
* Production SIEM integration

---

# Tech Stack

* Python
* XGBoost
* Ollama
* LLM Agents
* JSON Logging
* Schema-Grounded Reasoning
* Cybersecurity Tool Orchestration

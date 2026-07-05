# ⚡ Sovereign Automation Hub: n8n Workflows

> *Centralized n8n workflow definitions for lab orchestration, security automation, infrastructure management, and autonomous incident response within the sovereign lab.*

Workflows are the orchestration layer. Every complex operation — from security scans to infrastructure deployment to incident response — is decomposed into modular, reusable n8n workflows that trigger automatically or on-demand.

---

## 🎯 Overview & Purpose

| Icon | Goal | Details |
|------|------|---------|
| 🔄 | **Workflow Orchestration** | Decompose complex operations into modular, reusable workflows |
| 🤖 | **Autonomous Execution** | Trigger workflows on schedule, webhook, or AI agent decision |
| 🔗 | **Service Integration** | Connect all lab services: Ollama, Prometheus, security tools, infra nodes |
| 📊 | **Multi-Step Operations** | Coordinate across security, infrastructure, and monitoring domains |
| ✅ | **Status** | ✅ Active — 8+ workflows operational, auto-triggered |

---

## 🛠️ Technology Stack

```text
🔧 Orchestration        ::  n8n (self-hosted)
🐳 Deployment           ::  Docker Compose
🤖 AI Integration       ::  Ollama, Gemini CLI bridge
🔌 Data Flow            ::  HTTP webhooks, REST APIs, direct node execution
🛡️ Security            ::  Credentials vault, encrypted triggers, SSH execution
📊 Monitoring           ::  Prometheus metrics export, log aggregation
```

---

## 📂 Repository Structure

```
n8n-automation-hub/
├── README.md                                    (this file)
├── workflows/                                   (Workflow definitions)
│   ├── autonomous-executor.json                AI-driven task execution
│   ├── pro-engineering-agent.json              Infrastructure task management
│   ├── master-integrated.json                  Central hub coordinating all services
│   ├── task-coordinator.json                   Priority-based task queuing
│   ├── security/
│   │   ├── log-analysis-workflow.json          Real-time log analysis
│   │   ├── threat-detection.json               Anomaly detection trigger
│   │   └── incident-response.json              Automated incident handling
│   ├── infrastructure/
│   │   ├── gpu-health-monitor.json             GPU cluster monitoring
│   │   ├── node-deployment.json                Automated node setup
│   │   └── backup-orchestration.json           Scheduled backup coordination
│   ├── monitoring/
│   │   ├── metric-collection.json              Prometheus data collection
│   │   ├── alert-aggregation.json              Centralized alerting
│   │   └── dashboard-update.json               Grafana dashboard refresh
│   └── examples/
│       ├── simple-webhook-trigger.json         Basic webhook example
│       └── multi-step-workflow.json            Complex workflow pattern
│
├── credentials/                                 (Credential templates)
│   ├── ollama-connection.json                  Ollama API credentials
│   ├── prometheus-scrape.json                  Prometheus settings
│   ├── ssh-hosts.json                          SSH key management
│   ├── github-api.json                         GitHub integration
│   └── [service-name].json                     Service credentials template
│
├── config/                                      (Configuration)
│   ├── n8n-env.example                         Environment variables template
│   ├── webhook-settings.yaml                   Webhook configuration
│   ├── workflow-triggers.yaml                  Trigger conditions
│   └── secrets-vault.encrypted                 Encrypted credential storage
│
├── templates/                                   (Reusable workflow components)
│   ├── http-request-template.json              HTTP request node setup
│   ├── error-handling.json                     Error trap & notification
│   ├── logging-template.json                   Structured logging
│   └── retry-strategy.json                     Retry logic with backoff
│
├── docs/                                        (Documentation)
│   ├── WORKFLOW_GUIDE.md                       Creating & editing workflows
│   ├── TRIGGER_SETUP.md                        Webhook, schedule, AI triggers
│   ├── INTEGRATION_GUIDE.md                    Service integrations (Ollama, SSH, etc)
│   ├── CREDENTIAL_MANAGEMENT.md                Managing secrets securely
│   └── EXAMPLES.md                             Real workflow examples
│
├── scripts/                                     (Automation & deployment)
│   ├── import-workflows.sh                     Bulk import workflows
│   ├── export-workflows.sh                     Backup workflows to JSON
│   ├── backup-n8n-data.sh                      Full n8n database backup
│   └── restore-workflows.sh                    Restore from backup
│
├── docker-compose.yml                          n8n self-hosted deployment
├── docker-compose.override.yml                 Local development overrides
└── requirements.txt                            Python dependencies (for helpers)
```

---

## 🔄 Core Workflows

### **🤖 Autonomous Executor** (`autonomous-executor.json`)
High-level task orchestration driven by AI agents.

**Triggers:**
- Webhook from Gemini CLI agent
- n8n schedule (every 5 minutes)
- Manual trigger via HTTP API

**Flow:**
```
Incoming Task (AI Agent or Webhook)
  ↓
Parse Task + Extract Parameters
  ↓
Route to Appropriate Workflow (Security / Infrastructure / Monitoring)
  ↓
Execute + Monitor Progress
  ↓
Aggregate Results
  ↓
Return to Caller + Log Outcome
```

---

### **⚙️ Pro Engineering Agent** (`pro-engineering-agent.json`)
Infrastructure operations: deployments, configuration, remediation.

**Capabilities:**
- SSH command execution on nodes
- Docker container management (restart, scale, logs)
- Service health checks & automatic recovery
- Configuration file updates
- Database operations (backups, restores)

---

### **🌐 Master Integrated Hub** (`master-integrated.json`)
Central coordination for multi-service operations connecting all lab services.

---

### **📋 Task Coordinator** (`task-coordinator-reference.json`)
Priority-based task queue management with duplicate prevention and resource distribution.

---

## 🛡️ Security & Monitoring Workflows

### **📊 Log Analysis Workflow** (`security/log-analysis-workflow.json`)
Real-time log aggregation and anomaly detection.

### **🚨 Threat Detection Workflow** (`security/threat-detection.json`)
Triggered by Morpheus or security agents on suspected threats.

### **🔴 Incident Response Workflow** (`security/incident-response.json`)
Automated response: Detection → Containment → Analysis → Remediation → Verification

---

## 🏗️ Infrastructure Workflows

### **💻 GPU Health Monitor** (`infrastructure/gpu-health-monitor.json`)
Continuous GPU cluster health tracking with automatic remediation on alerts.

### **🚀 Node Deployment Workflow** (`infrastructure/node-deployment.json`)
Automated node setup from bare metal to operational cluster member.

---

## 📊 Monitoring Workflows

### **📈 Metric Collection Workflow** (`monitoring/metric-collection.json`)
Aggregate Prometheus metrics from all nodes every 30 seconds.

### **🚨 Alert Aggregation Workflow** (`monitoring/alert-aggregation.json`)
Centralize alerts, deduplicate, score severity, notify team.

---

## 🔌 Service Integrations

- **Ollama LLM Calls** — AI-driven analysis and decision making
- **SSH Command Execution** — Direct node operations
- **Prometheus Queries** — Metrics-driven automation
- **Webhook Triggers** — Event-driven workflows

---

## 🚀 Deployment

### Prerequisites
- Docker & Docker Compose
- Port 5678 available
- SSH keys for node access
- Ollama running on port 11434

### Quick Start

```bash
# Clone repository
git clone https://github.com/Dinaverse/n8n-automation-hub
cd n8n-automation-hub

# Configure environment
cp config/n8n-env.example .env

# Start n8n
docker-compose up -d

# Access UI
open http://localhost:5678
```

### Import Workflows

```bash
./scripts/import-workflows.sh
```

---

## 📖 Workflow Development

### Creating a New Workflow

1. Open n8n UI → Click "+" → Create New Workflow
2. Add Trigger (Webhook, Schedule, Manual)
3. Build Steps (HTTP, SSH, Logic, etc)
4. Add Error Handling
5. Test execution
6. Export: `./scripts/export-workflows.sh`
7. Commit to Git

---

## 🐛 Troubleshooting

### Workflow timeout
**Symptoms:** Workflow stalls after 5 minutes
```bash
docker logs n8n-automation-hub_app_1
# Edit workflow > Settings > Timeout
```

### SSH connection fails
```bash
ssh-add ~/.ssh/id_lab_master
ssh -i ~/.ssh/id_lab_master dina@arch-gpu-01
```

### Ollama not responding
```bash
curl http://localhost:11434/api/tags
docker restart ollama
nvidia-smi
```

---

## ✅ Operational Status

| Workflow | Status | Trigger | Last Run |
|----------|--------|---------|----------|
| Autonomous Executor | ✅ Active | Webhook + Schedule | 2026-07-05 12:34 |
| Engineering Agent | ✅ Active | Manual + Auto-remediation | 2026-07-05 11:22 |
| Master Integrated | ✅ Active | Continuous | 2026-07-05 12:50 |
| Task Coordinator | ✅ Active | Queue | 2026-07-05 12:48 |
| Log Analysis | ✅ Active | Every 10m | 2026-07-05 12:45 |
| Threat Detection | ✅ Active | Webhook | 2026-07-05 12:30 |
| GPU Health Monitor | ✅ Active | Every 5m | 2026-07-05 12:50 |
| Alert Aggregation | ✅ Active | Event-driven | 2026-07-05 12:50 |

---

## 📚 Documentation

| Document | Purpose |
|----------|---------|
| [WORKFLOW_GUIDE.md](docs/WORKFLOW_GUIDE.md) | Creating and editing workflows |
| [TRIGGER_SETUP.md](docs/TRIGGER_SETUP.md) | Configuring triggers |
| [INTEGRATION_GUIDE.md](docs/INTEGRATION_GUIDE.md) | Service integrations |
| [CREDENTIAL_MANAGEMENT.md](docs/CREDENTIAL_MANAGEMENT.md) | Credential storage |
| [EXAMPLES.md](docs/EXAMPLES.md) | Real workflow examples |

---

## 🔗 Integration with Dinaverse Ecosystem

| Component | Repository | Integration | Purpose |
|-----------|-----------|-------------|---------|
| **AI Skills** | [sovereign-ai-skills](https://github.com/Dinaverse/sovereign-ai-skills) | Skills triggered by workflows | Encode domain expertise |
| **Security Automation** | [cybersecurity-lab-automation](https://github.com/Dinaverse/cybersecurity-lab-automation) | Incident response triggers | Orchestrate security responses |
| **Infrastructure** | [sovereign-ai-infrastructure](https://github.com/Dinaverse/sovereign-ai-infrastructure) | Node orchestration | Lab-wide coordination |
| **Local AI Stack** | [local-ai-sovereign-stack](https://github.com/Dinaverse/local-ai-sovereign-stack) | Ollama integration | LLM execution |
| **Master Profile** | [Dinaverse](https://github.com/Dinaverse/Dinaverse) | Ecosystem hub | Central documentation |

---

## 🎯 Philosophy

> *Workflows are the nervous system of the lab. Every operation should be automated, auditable, and resilient.*

---

*Orchestrating autonomous operations. No cloud. No manual intervention. Full visibility.*

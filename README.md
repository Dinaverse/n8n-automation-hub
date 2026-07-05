# ⚡ Sovereign Automation Hub: n8n Workflows

> *Centralized n8n workflow definitions for lab orchestration, security automation, infrastructure management, and autonomous incident response within the sovereign lab.*

Workflows are the orchestration layer. Every complex operation — from security scans to infrastructure deployment to incident response — is decomposed into modular, reusable n8n workflows that execute autonomously based on schedules, webhooks, or AI agent decisions.

---

## 🎯 Overview & Purpose

| Icon | Goal | Details |
|------|------|----------|
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
│   │   └── backup-orchestrator.json            Distributed backup coordination
│   └── ai-integration/
│       ├── ollama-inference.json               LLM task dispatch
│       ├── gemini-cli-bridge.json              External AI integration
│       └── model-training-pipeline.json        Automated fine-tuning
├── credentials/                                 (Encrypted credential templates)
│   ├── ssh-keys.template                       Node SSH access
│   ├── api-tokens.template                     Service API credentials
│   └── prometheus.template                     Monitoring auth
├── triggers/                                    (Webhook & schedule configs)
│   ├── webhooks/
│   │   ├── github-events.json                  GitHub webhook listener
│   │   ├── alert-receiver.json                 Security alert ingestion
│   │   └── manual-dispatch.json                On-demand execution
│   └── schedules/
│       ├── hourly-monitoring.json              Hourly health checks
│       ├── daily-reports.json                  Daily summary generation
│       └── weekly-maintenance.json             Weekly infrastructure tasks
├── docker-compose.yml                          n8n stack deployment
└── docs/
    ├── DEPLOYMENT.md                           Setup & configuration guide
    ├── WORKFLOW_GUIDE.md                       Workflow design patterns
    └── INTEGRATION.md                          Service integration reference
```

---

## 🚀 Core Workflows

### 🤖 **Autonomous Executor** (`autonomous-executor.json`)
- **Purpose:** Central AI-driven workflow executor
- **Trigger:** AI agent decisions, manual dispatch webhooks
- **Actions:**
  - Accept task definitions from Gemini CLI
  - Decompose into n8n sub-workflows
  - Execute with error handling & retry logic
  - Return results to agent for decision-making
- **Integrations:** Ollama, SSH nodes, Prometheus, logging system

### 📋 **Pro Engineering Agent** (`pro-engineering-agent.json`)
- **Purpose:** Infrastructure task management & orchestration
- **Trigger:** Hourly schedule, infrastructure alerts
- **Actions:**
  - Monitor all lab nodes for health/performance
  - Detect capacity constraints
  - Trigger automated scaling/rebalancing
  - Generate capacity reports
- **Integrations:** Node SSH, Prometheus, alerting system

### 🔒 **Security & Threat Detection**
- **Real-time Log Analysis:** Parse Suricata IDS, system logs, application logs
- **Threat Detection:** Pattern matching, anomaly scoring, alert enrichment
- **Incident Response:** Auto-escalation, evidence collection, remediation workflows
- **Integrations:** Suricata, Prometheus, email alerts, Slack webhooks

### 💾 **Infrastructure Management**
- **GPU Health Monitor:** Track NVIDIA GPU utilization, temperature, errors
- **Node Deployment:** Automated provisioning via Proxmox/LXC
- **Backup Orchestrator:** Distributed backup scheduling, verification, retention
- **Integrations:** Proxmox API, NVIDIA monitoring, distributed storage

### 🧠 **AI Integration Layer**
- **Ollama Inference:** Dispatch tasks to local LLM cluster
- **Gemini CLI Bridge:** External AI model integration
- **Model Training Pipeline:** Fine-tuning automation on GPU cluster
- **Integrations:** Ollama API, Gemini CLI, CUDA nodes

---

## ⚙️ Execution Flow

```
┌────────────────────────────────────────────────────────────────────────────┐
│                      Trigger Sources                             │
│  ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────────────┐ │
│  │ AI Agent    │  │   Webhooks   │  │  Cron Schedules      │ │
│  │ Decisions   │  │  (GitHub,    │  │  (Hourly, Daily,     │ │
│  │             │  │   Alerts)    │  │   Weekly)            │ │
│  └──────┬──────┘  └──────┬──────┘  └──────┬─────────────────┘ │
│         │                │                 │                │
└─────────┼─────────────────┼─────────────────┼────────────────┘
          │                │                 │
          └────────────────┼─────────────────┘
                          │
              ┌───────────▼──────────┐
              │   n8n Workflow Engine    │
              │  (Decision Logic)        │
              └───────────┬──────────┘
                          │
        ┌─────────────────┼────────────────────┐
        │                 │                  │
   ┌────▼────┐      ┌────────────┐    ┌──────▼──┐
   │Security │      │Infrastructure│   │ AI Task │
   │Workflows│      │  Workflows   │   │ Dispatch│
   └────┬────┘      └────┬────────┘    └──────┬──┘
        │                │                 │
        └────────────────┼─────────────────┘
                        │
            ┌──────────▼─────────┐
            │ Lab Nodes & │
            │ External Services     │
            └─────────────────────┘
```

---

## 🔐 Webhook Integration Points

### GitHub Events
- Endpoint: `/webhook/github-events`
- Triggers: Push, PR, Release, Issue
- Use Case: Auto-deploy updates, trigger security scans

### Security Alerts
- Endpoint: `/webhook/alert-receiver`
- Triggers: IDS alerts, log anomalies, system warnings
- Use Case: Immediate incident response

### Manual Dispatch
- Endpoint: `/webhook/manual-dispatch`
- Payload: `{ task: string, params: object }`
- Use Case: Ad-hoc workflow execution

---

## 📊 Monitoring & Metrics

All n8n workflows export Prometheus metrics:

```
n8n_workflow_executions_total          # Total workflow runs
n8n_workflow_duration_seconds          # Execution time
n8n_workflow_errors_total              # Failed executions
n8n_task_queue_depth                   # Pending tasks
n8n_node_execution_time                # Individual node timing
```

Dashboard available at: `http://<dell-precision-ip>:3100` (Grafana)

---

## 🚀 Deployment

### Prerequisites
- Docker & Docker Compose
- SSH access to all lab nodes
- Ollama running on Arch cluster
- Prometheus for metrics collection

### Quick Start

```bash
# 1. Clone the repository
git clone https://github.com/Dinaverse/n8n-automation-hub.git
cd n8n-automation-hub

# 2. Copy credential templates
cp credentials/*.template credentials/
# Edit with your actual credentials

# 3. Start n8n stack
docker-compose up -d

# 4. Access n8n UI
# Open: http://localhost:5678

# 5. Import workflows
# Copy JSON files from ./workflows/ into n8n UI
```

### Configuration

Edit `docker-compose.yml` to set:
- `N8N_HOST`: Your orchestration node hostname/IP
- `N8N_PORT`: Port for n8n UI (default 5678)
- `DB_TYPE`: postgres (recommended for production)
- `OLLAMA_API`: Arch cluster Ollama endpoint
- `PROMETHEUS_SCRAPE`: Dell precision monitoring endpoint

---

## 🔐 Security Considerations

1. **Credentials Storage**
   - Store all credentials in n8n's encrypted vault
   - Never commit credentials to Git
   - Use `.template` files for sharing

2. **Workflow Authorization**
   - Restrict webhook access via IP allowlisting
   - Use signed webhook payloads where applicable
   - Audit all external integrations

3. **Execution Isolation**
   - Run workflows in isolated containers
   - Use dedicated SSH keys per node
   - Implement rate limiting on popular workflows

---

## 📈 Integration Map

```
n8n-automation-hub
    ├── [Ollama] local-ai-sovereign-stack
    ├── [Monitoring] sovereign-ai-infrastructure
    ├── [Security] cybersecurity-lab-automation
    ├── [Skills] sovereign-ai-skills
    └── [Lab Nodes] my-sovereign-lab
```

---

## 🛠️ Development & Contributing

### Adding a New Workflow

1. Design workflow logic in n8n UI
2. Export JSON from n8n
3. Add to appropriate subdirectory (`workflows/security/`, etc.)
4. Document in `docs/WORKFLOW_GUIDE.md`
5. Test in staging before production deployment
6. Commit with descriptive message

### Testing Workflows

```bash
# Run workflow via CLI
n8n execute --file workflows/security/log-analysis-workflow.json

# Test webhook payload
curl -X POST http://localhost:5678/webhook/manual-dispatch \
  -H "Content-Type: application/json" \
  -d '{"task":"test-task","params":{}}'
```

---

## 📞 Support & Debugging

- **Logs:** `docker logs n8n`
- **Status:** UI available at `http://localhost:5678`
- **Metrics:** Check Prometheus for workflow performance
- **Issues:** Check GitHub Issues for known problems

---

*Orchestrating the sovereign lab through modular, autonomous workflows.*
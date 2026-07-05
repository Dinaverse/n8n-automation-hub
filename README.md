# ⚡ Sovereign Automation Hub: n8n Workflows

> *Centralized n8n workflow definitions for lab orchestration, security automation, infrastructure management, and autonomous incident response within the sovereign lab.*

Workflows are the orchestration layer. Every complex operation — from security scans to infrastructure deployment to incident response — is decomposed into modular, reusable n8n workflows that execute autonomously or via AI agent trigger.

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

**Capabilities:**
- Task classification and routing
- Parameter validation and sanitization
- Parallel execution of independent tasks
- Result aggregation and error handling
- Structured logging for audit trails

---

### **⚙️ Pro Engineering Agent** (`pro-engineering-agent.json`)
Infrastructure operations: deployments, configuration, remediation.

**Capabilities:**
- SSH command execution on nodes
- Docker container management (restart, scale, logs)
- Service health checks & automatic recovery
- Configuration file updates via templating
- Database operations (backups, restores, migrations)
- Log aggregation and analysis
- Performance metric collection

**Supported Operations:**
- Create/destroy containers
- Deploy configurations to multiple hosts
- Execute maintenance routines
- Rollback failed deployments

---

### **🌐 Master Integrated Hub** (`master-integrated.json`)
Central coordination for multi-service operations connecting all lab services.

**Features:**
- Unified service orchestration across all lab components
- Real-time status aggregation from all nodes
- Centralized event logging and correlation
- Cross-service dependency management
- Automated failover and recovery coordination

**Integration Points:**
- Ollama LLM inference cluster
- Prometheus metrics collection
- Suricata IDS threat detection
- Docker container fleet
- SSH node management
- GitHub repository workflows

---

### **📋 Task Coordinator** (`task-coordinator.json`)
Priority-based task queue management with duplicate prevention and resource distribution.

**Features:**
- Priority-based task queuing (High/Normal/Low)
- Duplicate task detection and consolidation
- Resource availability checking before execution
- Fair load distribution across nodes
- Task timeout and retry management
- Historical task tracking and analytics

---

## 🛡️ Security & Monitoring Workflows

### **📊 Log Analysis Workflow** (`security/log-analysis-workflow.json`)
Real-time log aggregation and anomaly detection.

**Functions:**
- Collect logs from all lab nodes via SSH/syslog
- Parse and normalize log formats
- Anomaly detection via statistical analysis
- Alert on threshold violations
- Export to central SIEM or Elasticsearch

---

### **🚨 Threat Detection Workflow** (`security/threat-detection.json`)
Triggered by Morpheus or security agents on suspected threats.

**Capabilities:**
- Network traffic analysis (via Suricata alerts)
- Behavioral anomaly detection
- Malware signature scanning
- Log pattern matching
- Cross-reference with threat intel databases
- Escalation to incident response workflows

---

### **🔴 Incident Response Workflow** (`security/incident-response.json`)
Automated response: Detection → Containment → Analysis → Remediation → Verification

**Steps:**
1. **Detection:** Receive alert from threat detection workflow
2. **Containment:** Isolate affected node/service
3. **Analysis:** Gather forensic data, logs, memory dumps
4. **Remediation:** Apply patches, restart services, restore from backup
5. **Verification:** Confirm remediation, return to normal operations
6. **Documentation:** Generate incident report with timeline

---

## 🏗️ Infrastructure Workflows

### **💻 GPU Health Monitor** (`infrastructure/gpu-health-monitor.json`)
Continuous GPU cluster health tracking with automatic remediation on alerts.

**Monitoring:**
- GPU temperature and power consumption
- Memory utilization across 4x P106-100 cluster
- CUDA process monitoring
- Driver stability checks
- Thermal throttling detection

**Automatic Actions:**
- Reduce compute load on high temp
- Restart stalled CUDA processes
- Alert on driver crashes
- Schedule maintenance windows

---

### **🚀 Node Deployment Workflow** (`infrastructure/node-deployment.json`)
Automated node setup from bare metal to operational cluster member.

**Stages:**
- OS provisioning and initial config
- Dependency installation
- Service deployment (Docker, monitoring agents)
- Network configuration and DNS registration
- Health verification and integration testing

---

## 📊 Monitoring Workflows

### **📈 Metric Collection Workflow** (`monitoring/metric-collection.json`)
Aggregate Prometheus metrics from all nodes every 30 seconds.

**Metrics Collected:**
- CPU, memory, disk utilization
- Network bandwidth and latency
- Docker container stats
- GPU metrics (temperature, power, utilization)
- Custom application metrics

---

### **🚨 Alert Aggregation Workflow** (`monitoring/alert-aggregation.json`)
Centralize alerts, deduplicate, score severity, notify team.

**Processing:**
- Alert deduplication (within 5-minute window)
- Severity scoring based on impact
- Alert correlation (related alerts grouped)
- Notification routing (email, Slack, webhook)
- Historical tracking and alerting trends

---

## 🔌 Service Integrations

| Service | Integration | Purpose |
|---------|-------------|----------|
| **Ollama LLM** | REST API (port 11434) | AI-driven analysis and decision making |
| **SSH Nodes** | SSH execution nodes | Direct node operations and commands |
| **Prometheus** | HTTP API (port 9090) | Metrics-driven automation and alerting |
| **GitHub** | REST API + webhooks | Repo management, issue automation, CI/CD |
| **Suricata IDS** | EVE JSON logs | Security event ingestion and triggering |
| **Docker** | Remote API | Container orchestration and management |
| **Grafana** | HTTP API | Dashboard updates and visualization |

---

## 🚀 Deployment

### Prerequisites
- Docker & Docker Compose (latest versions)
- Port 5678 available (n8n UI)
- SSH keys for node access configured
- Ollama running on port 11434
- Prometheus running and scraping all nodes
- Firewall rules allowing webhook ingress

### Quick Start

```bash
# Clone repository
git clone https://github.com/Dinaverse/n8n-automation-hub.git
cd n8n-automation-hub

# Copy environment template
cp config/n8n-env.example .env

# Edit .env with your settings
nano .env

# Start n8n with Docker Compose
docker-compose up -d

# Access n8n UI
open http://localhost:5678
```

### Initial Setup

1. **Import Workflows:**
   ```bash
   bash scripts/import-workflows.sh
   ```

2. **Configure Credentials:**
   - Navigate to Credentials in n8n UI
   - Add SSH host credentials
   - Add Ollama connection details
   - Configure GitHub PAT, Prometheus endpoints

3. **Enable Triggers:**
   - Activate webhooks in trigger nodes
   - Set scheduling for periodic workflows
   - Test manual execution first

4. **Verify Integrations:**
   - Test SSH connectivity to all nodes
   - Verify Ollama inference response times
   - Check Prometheus metric scraping
   - Validate webhook payload delivery

---

## 📋 Backup & Recovery

### Backup Workflows
```bash
bash scripts/export-workflows.sh backup-$(date +%Y%m%d).json
```

### Backup Full n8n Data
```bash
bash scripts/backup-n8n-data.sh
```

### Restore from Backup
```bash
bash scripts/restore-workflows.sh backup-20260705.json
```

---

## 🔐 Security Best Practices

1. **Credentials Management:**
   - Use n8n's encrypted credential vault
   - Rotate SSH keys and API tokens regularly
   - Never commit credentials to version control

2. **Webhook Security:**
   - Enable webhook authentication tokens
   - Use HTTPS for webhook URLs
   - IP whitelist webhook sources

3. **Audit Logging:**
   - Enable n8n audit logs
   - Export logs to centralized SIEM
   - Monitor workflow execution history

4. **Access Control:**
   - Restrict n8n UI access via SSH tunnel or VPN
   - Use strong authentication for n8n accounts
   - Implement role-based access control

---

## 📈 Performance Tuning

- **Concurrency:** Set worker threads based on available CPU cores
- **Memory:** Allocate sufficient memory for large workflow executions
- **Database:** Use PostgreSQL backend for production (not SQLite)
- **Caching:** Enable Redis caching for frequently accessed data
- **Monitoring:** Use Prometheus to track workflow execution times

---

## 🛠️ Troubleshooting

| Issue | Cause | Solution |
|-------|-------|----------|
| Workflow hangs | SSH timeout or service unavailable | Check node connectivity, increase timeouts |
| Webhook not triggered | Firewall blocking inbound traffic | Verify port 5678 open, check firewall rules |
| Ollama inference slow | GPU memory exhaustion | Check GPU utilization, reduce batch size |
| Credential errors | Token expired or misconfigured | Rotate credentials, verify connection settings |

---

## 📚 Documentation

- **[Workflow Creation Guide](docs/WORKFLOW_GUIDE.md)** — Creating and editing workflows
- **[Trigger Setup](docs/TRIGGER_SETUP.md)** — Configuring webhooks, schedules, and AI triggers
- **[Integration Guide](docs/INTEGRATION_GUIDE.md)** — Service integrations and API connections
- **[Credential Management](docs/CREDENTIAL_MANAGEMENT.md)** — Secure credential handling
- **[Examples](docs/EXAMPLES.md)** — Real-world workflow examples and patterns

---

## 🔗 Related Repositories

| Repository | Purpose |
|------------|----------|
| [`sovereign-ai-infrastructure`](https://github.com/Dinaverse/sovereign-ai-infrastructure) | Lab infrastructure documentation |
| [`my-sovereign-lab`](https://github.com/Dinaverse/my-sovereign-lab) | Lab master documentation |
| [`cybersecurity-lab-automation`](https://github.com/Dinaverse/cybersecurity-lab-automation) | Security automation tooling |
| [`local-ai-sovereign-stack`](https://github.com/Dinaverse/local-ai-sovereign-stack) | Ollama & AI stack deployment |

---

## 📊 Status Dashboard

| Workflow | Status | Last Run | Next Run |
|----------|--------|----------|----------|
| Autonomous Executor | ✅ Active | Today 14:32 | 5min |
| Pro Engineering Agent | ✅ Active | Today 13:15 | On-demand |
| Master Integrated Hub | ✅ Active | Today 14:00 | 1min |
| Log Analysis | ✅ Active | Today 14:35 | Real-time |
| GPU Health Monitor | ✅ Active | Today 14:30 | 30sec |
| Incident Response | ✅ Standby | Yesterday 09:20 | On-alert |

---

*Orchestrating resilience through automation. Every workflow is a step toward autonomous infrastructure.*

# 📊 Grafana 12.x + Prometheus SNMP Monitoring Stack

This repository showcases a full-stack observability solution using **Grafana 12.x**, **Prometheus**, and **SNMP v1/v2** to monitor infrastructure across:

- 🖧 Switches & Routers  
- 🖥️ Servers & Operating Systems  
- 🗄️ Databases  
- ☸️ Kubernetes Clusters  
- 🧩 Applications  

It includes dashboards, alerting rules, scrape configs, SNMP modules, and a runbook for operational use.

---

## 🧱 Architecture Overview

```text
[ SNMP Devices (v1/v2) ] → [ snmp_exporter ] → [ Prometheus ] → [ Grafana 12.x ]
                                        ↑
                          [ snmp.yml + generator.yml ]

📦 Repository Structure
Code
grafana-prometheus-snmp-monitoring/
├── prometheus.yml         # Prometheus scrape config
├── generator.yml          # SNMP module definitions
├── snmp.yml               # SNMP exporter config (generated)
├── alerts.yml             # Prometheus alert rules
├── dashboards/            # Grafana dashboard JSONs
│   ├── switches.json
│   ├── servers.json
│   ├── databases.json
│   ├── kubernetes.json
│   └── applications.json
├── runbook.md             # Operational runbook (Markdown format)
└── README.md              # This file
🚀 Setup Instructions
1. Clone the Repo
bash
git clone https://github.com/omgwarrior/grafana-prometheus-snmp-monitoring.git
cd grafana-prometheus-snmp-monitoring
2. Generate snmp.yml (Optional)
If you want to regenerate snmp.yml from generator.yml:

bash
docker run -v $(pwd):/opt snmp-generator generate
3. Start SNMP Exporter
bash
docker run -d -p 9116:9116 \
  -v $(pwd)/snmp.yml:/etc/snmp_exporter/snmp.yml \
  prom/snmp-exporter
4. Start Prometheus
bash
docker run -d -p 9090:9090 \
  -v $(pwd)/prometheus.yml:/etc/prometheus/prometheus.yml \
  prom/prometheus
5. Start Grafana
bash
docker run -d -p 3000:3000 grafana/grafana
6. Import Dashboards
Go to Grafana → Dashboards → Import

Upload JSON files from dashboards/

📊 Dashboards Included
Dashboard	Metrics Visualized
switches.json	Interface traffic, errors, uptime, port status
servers.json	CPU load, memory usage, disk I/O, uptime
databases.json	Query rate, buffer pool, disk usage, connections
kubernetes.json	Pod status, node health, container restarts
applications.json	API latency, error rate, uptime, custom metrics
Each dashboard uses PromQL queries and templating ($instance, $namespace) for dynamic reuse.

🔔 Alerting
Prometheus alert rules are defined in alerts.yml. Example:

yaml
- alert: HighCPUUsage
  expr: load1 > 5
  for: 5m
  labels:
    severity: warning
  annotations:
    summary: "High CPU load detected"
Grafana also supports panel-based alerting with contact points and notification policies.

📋 Runbook
See runbook.md for:

Setup checklist

SNMP device onboarding

Alert tuning procedures

Troubleshooting steps

🎥 Tutorials That Reinforce This Stack
Prometheus SNMP Exporter: Network Monitoring Tutorial!

Monitoring Networks with Prometheus and the SNMP exporter

Setting up Prometheus and Grafana for monitoring your servers

Kubernetes Monitoring with Prometheus and Grafana

Monitoring Your Kubernetes Cluster with Grafana

Network Monitoring with Prometheus and Grafana | Martin Le

✅ Supported SNMP Modules
Defined in generator.yml and snmp.yml:

switches: Interface stats, uptime, port status

routers: IP and TCP tables

servers: CPU, memory, disk, uptime

databases: Disk I/O, query rate, connections

os: hrSystemUptime, hrStorageTable, hrProcessorTable

kubernetes: Node stats, uptime

applications: Custom OIDs for uptime, latency, errors

🛡️ Security Notes
SNMP v2c is used with community: public for demo purposes

For production, use SNMPv3 with authentication and encryption

Secure Grafana and Prometheus with RBAC and TLS

🙌 Author
Built by Alvin Cly – Sr. DevOps & SRE Engineer GitHub: omgwarrior LinkedIn: linkedin.com/in/alvincly

📬 Contributions & Feedback
Feel free to fork, submit PRs, or open issues. Feedback and improvements are welcome!

Code

Let me know if you want to add badges, CI/CD integration, or a demo GIF. This README is ready to go—just drop it into your repo and hit push. Let’s make this project shine.
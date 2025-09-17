# grafana-prometheus-snmp-monitoring
GitHub repo to showcase Grafana 12.x + Prometheus + SNMP pull-based monitoring.
# Grafana 12.x + Prometheus SNMP Monitoring

This repository showcases a full-stack observability setup using Grafana 12.x and Prometheus to monitor SNMP-enabled infrastructure across network devices, servers, databases, Kubernetes clusters, and applications.

## 🔧 Stack Overview

- **Grafana 12.x** – Visualization and alerting
- **Prometheus** – Metrics collection and querying
- **SNMP Exporter** – Pull-based SNMP metrics
- **SNMP v1/v2** – Supported protocols
- **Docker** – Containerized deployment

## 📦 Components

- `prometheus.yml`: Prometheus scrape config
- `generator.yml`: SNMP module definitions
- `snmp.yml`: Generated SNMP exporter config
- `dashboards/`: Grafana JSON dashboards
- `runbook.xlsx`: Operational runbook
- `alerts.yml`: Prometheus alert rules

## 🚀 Setup Instructions

### 1. Clone the Repo

```bash
git clone https://github.com/omgwarrior/grafana-prometheus-snmp-monitoring.git
cd grafana-prometheus-snmp-monitoring

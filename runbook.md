# SNMP Monitoring Runbook

| Step | Target | Description | Command | Expected Output | Notes |
|------|--------|-------------|---------|-----------------|-------|
| 1 | All | Clone repo | `git clone ...` | Repo ready | Include README |
| 2 | SNMP | Generate config | `generator --config=generator.yml` | `snmp.yml` created | Use correct MIBs |
| 3 | SNMP Exporter | Start container | `docker run -p 9116:9116 ...` | Exporter running | Confirm `/metrics` |
| 4 | Prometheus | Configure scrape | Edit `prometheus.yml` | Targets scraped | Validate `/targets` |
| 5 | Grafana | Start UI | `docker run -p 3000:3000 ...` | Grafana running | Default creds: admin/admin |
| 6 | Grafana | Import dashboards | Upload JSON | Metrics visible | Use templating |
| 7 | All | Create alerts | Panel → Alert tab | Notifications sent | Test with dummy data |

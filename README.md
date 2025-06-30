# Docker Log Aggregation Stack

This repository provides a simple docker-compose configuration for a centralized logging and monitoring stack. It includes **syslog-ng**, **Prometheus**, **Grafana**, **cAdvisor**, and **Node Exporter**.

## Folder Structure

```
conf/
  syslog-ng/syslog-ng.conf       # syslog-ng configuration
  prometheus/prometheus.yml      # Prometheus scrape configuration
  grafana/
    provisioning/
      datasources/datasource.yml # Grafana datasource for Prometheus
      dashboards/dashboard.yml   # Dashboard provisioning

logs/
  syslog-ng/                     # persistent log storage

dashboards/
  container_overview.json        # sample Grafana dashboard
```

## Usage

1. Start the stack:

```bash
docker-compose up -d
```

2. Send test logs:

```bash
logger -n 127.0.0.1 -P 514 "test message from host"
```

3. Access Grafana at [http://localhost:3000](http://localhost:3000) (admin/admin). The `Container Overview` dashboard is preloaded.

4. Prometheus metrics are available at [http://localhost:9090](http://localhost:9090).

Logs collected by syslog-ng are stored under `logs/syslog-ng/`.

## Notes

- Containers are configured with the syslog logging driver to automatically forward their stdout/stderr to syslog-ng.
- Modify or add dashboards in the `dashboards/` directory and they will be automatically loaded by Grafana.

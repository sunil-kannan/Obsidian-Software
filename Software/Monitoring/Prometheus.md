---
date: "2025-11-20"
tags: 
link:
---
# Prometheus – Notes

## ⭐ Overview

Prometheus is an open-source **monitoring and alerting** system designed for reliability and scalability. It collects metrics, stores them in a time-series database, and lets you query them using **PromQL**.

![[prometheus.gif]]


---

## 🏗 Architecture Components

### 1. **Prometheus Server**

- The core component.
- Scrapes metrics from targets.
- Stores metrics locally in a time-series DB.
- Runs PromQL queries.

### 2. **Exporters**

- Applications expose metrics via `/metrics` endpoint.
- Exporters convert system/app metrics → Prometheus format.
- Examples:
    
    - Node exporter (Linux/Windows metrics)
    - JMX exporter (Java apps)
    - Blackbox exporter (probes HTTP/TCP/etc.)

### 3. **Pushgateway**

- Used when a service cannot be scraped (short-lived jobs).
- Services push metrics to Pushgateway → Prometheus scrapes it.

### 4. **Alertmanager**

- Sends alerts via email, Slack, PagerDuty, etc.
- Handles alert grouping, silencing, throttling.

### 5. **Grafana (Optional)**

- Visualization tool.
- Prometheus acts as a datasource.


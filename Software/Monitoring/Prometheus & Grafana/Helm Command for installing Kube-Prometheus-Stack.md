---
date: 2025-11-19
tags:
link:
---
# Helm Command for installing Kube-Prometheus-Stack

> This command installs Prometheus + Grafana + Alertmanager, and enables the experimental remote write endpoint so k6 (or any other client) can send metrics to it.


Add Prometheus Helm repository
```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```


  
Install kube-prometheus-stack (includes Prometheus + Grafana)
```
helm upgrade --install prometheus prometheus-community/kube-prometheus-stack \
  --namespace monitoring \
  --create-namespace \
  --set grafana.adminPassword=admin \
  --set prometheus.service.type=ClusterIP \
  --set grafana.service.type=ClusterIP \
  --set alertmanager.service.type=ClusterIP \
  --set prometheus.prometheusSpec.enableRemoteWriteReceiver=true \
  --set prometheus.prometheusSpec.enableFeatures[0]=remote-write-receiver
  --set prometheus.prometheusSpec.enableFeatures[1]=web.enable-remote-write-receiver
```

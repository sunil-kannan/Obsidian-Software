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


#### Exposing the Prometheus and Grafana UI using Kubernetes ingress

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: prometheus-ingress
  namespace: monitoring
spec:
  ingressClassName: nginx  	
  rules:
  - host: prometheus.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: prometheus-kube-prometheus-prometheus
            port:
              number: 9090

```

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: grafana-ingress
  namespace: monitoring
spec:
  ingressClassName: nginx  	
  rules:
  - host: grafana.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: prometheus-grafana
            port:
              number: 80

```
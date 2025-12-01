---
date: 2025-11-29
tags:
link:
---






grafana:
  adminPassword: admin
  service:
    type: ClusterIP

prometheus:
  service:
    type: ClusterIP
  prometheusSpec:
    enableRemoteWriteReceiver: true
    enableFeatures:
      - remote-write-receiver
    serviceMonitorSelectorNilUsesHelmValues: false
    podMonitorSelectorNilUsesHelmValues: false

alertmanager:
  service:
    type: ClusterIP
  alertmanagerSpec:
    replicas: 1
  
  # CORRECTED ALERTMANAGER CONFIG
  config:
    global:
      resolve_timeout: 5m

    route:
      receiver: 'discord'
      group_by: ['alertname']
      group_wait: 10s
      group_interval: 10s
      repeat_interval: 1h
      
      # Add specific routes for different alerts
      routes:
        - receiver: 'discord'
          match:
            alertname: 'K6HighLatencyMax'
          group_wait: 10s
          group_interval: 10s
          repeat_interval: 5m
          
        - receiver: 'discord'
          match_re:
            severity: 'warning|critical'
          group_wait: 10s
          group_interval: 10s
          repeat_interval: 1h


    receivers:
      - name: 'discord'
        webhook_configs:
          - url: "https://discord.com/api/webhooks/1443473720604758167/uPhTCFKrDk16tUE4OItkqSXdua5w-vXBNgl3SdHRcUcIPCvAI0FTFAdWj5vXy8aiVX0M"
            send_resolved: true
            http_config:
              follow_redirects: true
            # Tell Alertmanager to POST the rendered template as the body.
            # Some Alertmanager versions accept `message` here; if yours does not,
            # we'll mount the template file and Alertmanager will use it automatically
            # to render the outgoing payload.
            # If your operator version supports it you can add:
            #   message: '{{ template "discord.default.message" . }}'




helm upgrade --install prometheus prometheus-community/kube-prometheus-stack   -n monitoring   -f values.yaml




apiVersion: v1
kind: ConfigMap
metadata:
  name: alertmanager-templates
  namespace: monitoring
data:
  discord.tmpl: |
    {{ define "discord.default.message" -}}
    {
      "content": "**ALERT**: {{ .CommonLabels.alertname }} is {{ .Status | toUpper }}\n
**Severity:** {{ .CommonLabels.severity }}\n
**Summary:** {{ .CommonAnnotations.summary }}\n
**Description:** {{ .CommonAnnotations.description }}\n
**Generator:** {{ .GeneratorURL }}"
    }
    {{- end }}

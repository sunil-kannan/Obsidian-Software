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
      group_interval: 30s
      repeat_interval: 2m
      receiver: "null"
      routes:
         # 1. Allow ONLY K6 alerts
        - match_re:
            alertname: "K6.*"   # ALL alerts starting with "K6"
          receiver: 'discord'

        # Drop EVERYTHING else

        - match_re:
            alertname: ".*"
        - receiver: 'null'

    receivers:
      - name: "discord"
        webhook_configs:
          - url: "http://alertmanager-discord-relay.monitoring.svc.cluster.local/alert"
            send_resolved: true

      - name: "null"









cat <<'EOF' | kubectl apply -f -
apiVersion: v1
kind: Secret
metadata:
  name: discord-webhook-secret
  namespace: monitoring
stringData:
  discord_url: "https://discord.com/api/webhooks/1443473720604758167/uPhTCFKrDk16tUE4OItkqSXdua5w-vXBNgl3SdHRcUcIPCvAI0FTFAdWj5vXy8aiVX0M"
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: alertmanager-discord-relay
  namespace: monitoring
data:
  app.py: |
    from flask import Flask, request
    import os, requests, json

    app = Flask(__name__)

    DISCORD_URL = os.getenv("DISCORD_URL")

    @app.route("/alert", methods=["POST"])
    def handle_alert():
        data = request.json

        if not data:
            return "No data", 400

        for alert in data.get("alerts", []):
            labels = alert.get("labels", {})
            annotations = alert.get("annotations", {})

            embed = {
                "title": f"🔥 {labels.get('alertname', 'Alert')}",
                "description": annotations.get("description", 'No description'),
                "fields": [
                    {"name": "Scenario", "value": labels.get("scenario", "N/A"), "inline": True},
                    {"name": "Test ID", "value": labels.get("testid", "N/A"), "inline": True},
                    {"name": "Severity", "value": labels.get("severity", "N/A"), "inline": True},
                    {"name": "Value", "value": annotations.get("value", "N/A"), "inline": True},
                ]
            }

            payload = {"embeds": [embed]}

            try:
                r = requests.post(DISCORD_URL, json=payload)
                print("Discord response:", r.text)
            except Exception as e:
                print("Error sending to Discord:", e)

        return "ok", 200

    if __name__ == "__main__":
        print("Starting Relay...")
        app.run(host="0.0.0.0", port=5000)

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: alertmanager-discord-relay
  namespace: monitoring
spec:
  replicas: 1
  selector:
    matchLabels:
      app: alertmanager-discord-relay
  template:
    metadata:
      labels:
        app: alertmanager-discord-relay
    spec:
      containers:
      - name: relay
        image: python:3.9-slim
        command: ["/bin/sh", "-c"]
        args:
          - |
            pip install flask requests && \
            echo "Starting Relay..." && \
            python /app/app.py
        env:
        - name: DISCORD_URL
          valueFrom:
            secretKeyRef:
              name: discord-webhook-secret
              key: discord_url
        volumeMounts:
        - name: relay-code
          mountPath: /app
        ports:
        - containerPort: 5000
      volumes:
      - name: relay-code
        configMap:
          name: alertmanager-discord-relay
---
apiVersion: v1
kind: Service
metadata:
  name: alertmanager-discord-relay
  namespace: monitoring
spec:
  selector:
    app: alertmanager-discord-relay
  ports:
    - port: 80
      targetPort: 5000
EOF

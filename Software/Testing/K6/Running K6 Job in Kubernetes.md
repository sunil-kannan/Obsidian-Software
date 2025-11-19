---
date: "2025-11-19"
tags: 
link:
---

# Running K6 Job in Kubernetes

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.




## Need to install Kube-Prometheus-Stack in Kubernetes
Install it using this [[Helm Command for installing Kube-Prometheus-Stack]]


### Create test script in configmap

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: k6-test-script
data:
  test.js: |
    import http from 'k6/http';
    import { check, sleep } from 'k6';
    import { Rate, Trend } from 'k6/metrics';

    const errorRate = new Rate('errors');
    const responseTimeTrend = new Trend('response_times');

    export const options = {
      stages: [
        { duration: '2m', target: 100 },
        { duration: '5m', target: 100 },
        { duration: '2m', target: 0 },
      ],
      thresholds: {
        http_req_duration: ['p(95)<500'],
        errors: ['rate<0.01'],
      },
    };

    export default function() {
      const response = http.get(`${__ENV.API_BASE_URL}/api/users`);
      
      const success = check(response, {
        'status is 200': (r) => r.status === 200,
        'response time OK': (r) => r.timings.duration < 1000,
      });
      
      errorRate.add(!success);
      responseTimeTrend.add(response.timings.duration);
      
      sleep(1);
    }
```
### Create Job for K6-Load test

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: k6-loadtest
  labels:
    app: k6-loadtest
spec:
  template:
    metadata:
      labels:
        app: k6-loadtest
    spec:
      containers:
      - name: k6
        image: grafana/k6:latest
        command:
        - "sh"
        - "-c"
        - |
          # Run test with Prometheus remote write
          k6 run \
            --out experimental-prometheus-rw \
            --tag testid=preprod-$(date +%s) \
            /test/test.js
        env:
        - name: K6_PROMETHEUS_RW_SERVER_URL
          value: "http://prometheus-operated.monitoring.svc.cluster.local:9090/api/v1/write"
        - name: K6_PROMETHEUS_RW_TREND_STATS
          value: "p(95),p(99),min,max"
        - name: API_BASE_URL
          valueFrom:
            secretKeyRef:
              name: preprod-urls
              key: api-base-url
        volumeMounts:
        - name: test-script
          mountPath: /test
      volumes:
      - name: test-script
        configMap:
          name: k6-loadtest-config
      restartPolicy: Never
```
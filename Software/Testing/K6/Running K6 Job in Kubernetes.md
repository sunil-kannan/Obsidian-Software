---
date: "2025-11-19"
tags: 
link:
---

# Running K6 Job in Kubernetes

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.




## Need to install Kube-Prometheus-Stack in Kubernetes

- Create seperate namespace in kubernetes called 'monitoring' 
- Next step = [[Helm Command for installing Kube-Prometheus-Stack]]. 
- Creating the below file and creating the pod in kubernetes.
- K6 load test results will be written to the prometheus 
- Using prometheus / Grafana we can view the load test result.


### Create test script in configmap

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: k6-loadtest-config
data:
  test.js: |
    import http from 'k6/http';
    import { check, sleep } from 'k6';
    import { Rate, Trend } from 'k6/metrics';

    const responseTime = new Trend('response_time_ms');
	const errorRate = new Rate('error_rate');
	const requestsCounter = new Counter('total_requests');
	const activeUsers = new Gauge('active_vusers');

	export const options = {
	  stages: [
		{ duration: '2m', target: 5 },   // Ramp up
		{ duration: '5m', target: 5 },   // Stay
		{ duration: '2m', target: 10 },  // Scale up
		{ duration: '5m', target: 10 },  // Stay
		{ duration: '2m', target: 0 },    // Ramp down
	  ],
	  thresholds: {
		http_req_duration: ['p(95)<500', 'p(99)<1000'],
		error_rate: ['rate<0.01'],
		response_time_ms: ['p(95)<500'],
	  },
	};

	export default function() {
	  activeUsers.add(1);
	  
	  const responses = http.batch([
		['GET', `${__ENV.API_BASE_URL}/api/v1/auth/guest-token`]
	  ]);
	  
	  // Track metrics
	  responses.forEach(response => {
		requestsCounter.add(1);
		responseTime.add(response.timings.duration);
		errorRate.add(response.status !== 200);
		
		check(response, {
		  'status is 200': (r) => r.status === 200,
		  'response time < 2s': (r) => r.timings.duration < 2000,
		});
	  });
	  
	  activeUsers.add(-1);
	  sleep(1);
	}
```

```shell
kubectl apply -f k6-loadtest-config.yml
```
### Create Secret key for url

```shell
kubectl create secret generic preprod-urls \
  --from-literal=api-base-url="https://your-api-url.example.com" \
  -n <namespace>
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


```shell
kubectl apply -f k6-loadtest.yml
```
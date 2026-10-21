# Kubernetes Monitoring Alerts

## 1. CPU Usage Alert

**Purpose:** Detects high CPU usage in pods within the `monitoring-demo` namespace.

**PromQL Query:**

```promql
sum by (pod) (
  rate(container_cpu_usage_seconds_total{
    namespace="monitoring-demo",
    container!="",
    container!="POD"
  }[1m])
)
```

- **Threshold:** Above 0.7 CPU cores
- **Evaluation interval:** 10 seconds
- **Pending period:** 0 seconds

**Testing:** CPU workload was generated to exceed the configured threshold. The alert fired in Grafana.

## 2. Pod Restart Alert

**Purpose:** Detects container restarts in the `monitoring-demo` namespace.

**PromQL Query:**

```promql
sum by (pod) (
  increase(kube_pod_container_status_restarts_total{
    namespace="monitoring-demo"
  }[5m])
)
```

- **Threshold:** Greater than 0 restarts
- **Evaluation window:** 5 minutes

**Testing:** A container was intentionally stopped to test restart detection. The restart count increased, the alert fired, and the pod returned to the Running and Ready state.

## 3. Email Notifications

Grafana email notifications were tested using Gmail SMTP. The notification configuration should use securely stored credentials rather than passwords committed to GitHub.

## 4. Verification

- Confirm alert rules are configured in Grafana.
- Generate CPU load and verify the CPU alert.
- Restart a test container and verify the pod restart alert.
- Check the alert state and email notification delivery.

**Note:** Alert thresholds and evaluation settings should match the actual configuration deployed in Grafana.

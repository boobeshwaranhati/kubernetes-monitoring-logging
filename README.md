# Kubernetes Monitoring and Centralized Logging

## Overview
A local Kubernetes monitoring and logging project using Prometheus, Grafana, Loki, and Grafana Alloy on Minikube.

## Tech Stack
- Minikube and Kubernetes
- Prometheus
- Grafana
- Loki
- Grafana Alloy
- Helm
- Nginx

## Architecture
- Prometheus collects Kubernetes metrics.
- Grafana visualizes metrics and manages alerts.
- Grafana Alloy collects container logs and forwards them to Loki.
- Grafana Explore is used to query and analyze logs.

## Project Structure
```text
├── Grafana dashboard export.json
│   └── 
├── docs/
│   └── alerts.md
├── helm/
│   ├── alloy-values.yaml
│   └── loki-values.yaml
├── k8s/
│   └── demo-app.yaml
├── screenshots/
├── .gitignore
└── README.md
```

## Features
- Kubernetes CPU and memory monitoring
- Pod status and container restart monitoring
- Centralized Nginx logs using Loki
- Grafana dashboards and alerting
- CPU usage and pod restart alert testing
- Email notification testing

## Setup
Prerequisites: Docker Desktop, Minikube, kubectl, and Helm.

Start the cluster and verify its status:
```powershell
minikube start
kubectl get nodes
kubectl get pods -A
```

Deploy the demo application:
```powershell
kubectl apply -f k8s/demo-app.yaml
```

Access Grafana:
```powershell
kubectl port-forward -n monitoring svc/monitoring-grafana 3000:80
```

Open http://localhost:3000.

## Log Query
Run this query in Grafana Explore with Loki selected:
```logql
{namespace="monitoring-demo", container="nginx"}
```

## Alerts
- **CPU usage:** Fires when the configured CPU threshold is exceeded.
- **Pod restarts:** Detects container restarts within the configured evaluation window.

See [docs/alerts.md](docs/alerts.md) for alert expressions and testing details.

## Dashboard
Import `dashboards/kubernetes-monitoring.json` into Grafana.

## Security
Never commit passwords, SMTP app passwords, tokens, or Kubernetes Secret manifests.

## Screenshots
Project screenshots are stored in the `screenshots/` directory.

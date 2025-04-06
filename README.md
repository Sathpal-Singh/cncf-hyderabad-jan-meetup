# 📊 Observability Demystified - CNCF Hyderabad Meetup

Welcome to the demo repository for my first-ever talk at **CNCF Hyderabad (January)**!

> 🔥 "Observability Demystified" covers how logs, metrics, and traces work together in Kubernetes, powered by the **Grafana Stack** (Prometheus, Loki, Tempo, Grafana).

---

## 🛠 Stack

- **Flask** Python app with Prometheus metrics and OpenTelemetry traces
- **Prometheus** for metrics
- **Loki** for logs
- **Tempo** for distributed tracing
- **Grafana** for visualization
- **Kubernetes** using Kind (or any cluster)

---

## 🚀 How to Run

1. Clone this repo:
    ```bash
    git clone https://github.com/Sathpal-Singh/observability-demystified.git
    cd observability-demystified
    ```

2. Start Kind + Monitoring Stack:
    ```bash
    kind create cluster
    helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
    helm repo add grafana https://grafana.github.io/helm-charts
    helm repo update
    helm install monitoring prometheus-community/kube-prometheus-stack --namespace monitoring --create-namespace
    helm install loki grafana/loki-stack --namespace logging --create-namespace --set promtail.enabled=true
    helm install tempo grafana/tempo --namespace tracing --create-namespace
    ```

3. Deploy Flask App:
    ```bash
    kubectl create namespace demo-app
    kubectl apply -f k8s/flask-app.yaml
    ```

4. Port-forward Grafana:
    ```bash
    kubectl port-forward svc/monitoring-grafana 3000:80 -n monitoring
    ```

5. Login Grafana (admin/admin), Add Loki and Tempo as Data Sources

6. Import `dashboards/flask-observability-dashboard.json`

7. See Metrics, Logs, and Traces live!

---

## 📚 References

- [Prometheus + Grafana Monitoring Stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack)
- [Grafana Loki (Logging)](https://grafana.com/oss/loki/)
- [Grafana Tempo (Tracing)](https://grafana.com/oss/tempo/)
- [OpenTelemetry Python](https://opentelemetry.io/docs/instrumentation/python/)

---

## 🤝 Connect with Me
- [LinkedIn](https://www.linkedin.com/in/sathpalsingh/)
- [GitHub](https://github.com/Sathpal-Singh)

---

# 🎉 Happy Observing!

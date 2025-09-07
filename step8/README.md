# Community Over Code NA 2025 K8ssandra workshop
## Step 8 - Observability


To install kube-prometheus-stack with our pre-defined demo values:


```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts --force-update
helm install prometheus prometheus-community/kube-prometheus-stack --namespace k8ssandra-operator -f kube-prom-stack-values.yaml
```

Create ServiceMonitor:

```
kubectl apply -f servicemonitor.yaml -n k8ssandra-operator
```

Access Prometheus UI from http://localhost:9090

```
kubectl port-forward svc/prometheus-operated -n k8ssandra-operator 9090:9090
```

Create Grafana dashboard:

```
kubectl apply -f grafana-dashboards-new.yaml -n k8ssandra-operator
```

Access Grafana from http://localhost:3000, the credentials are admin/secret

```
kubectl port-forward svc/prometheus-grafana -n k8ssandra-operator 3000:80
```

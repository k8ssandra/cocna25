# Community Over Code NA 2025 K8ssandra workshop
## Step 8 - Observability

To install kube-prometheus-stack with our pre-defined demo values enabling the remote write endpoint in Prometheus:


```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts --force-update
helm install prometheus prometheus-community/kube-prometheus-stack --namespace k8ssandra-operator -f ./step8/kube-prom-stack-values.yaml
```

Enable telemetry in the K8ssandraCluster, with some custom Vector pipelines:

```
kubectl apply -f ./step8/k8ssandra-cluster.yaml -n db
```

Access Prometheus UI from http://localhost:9090

```
kubectl port-forward svc/prometheus-operated -n k8ssandra-operator 9090:9090
```

Create the Grafana dashboards:

```
kubectl apply -f ./step8/grafana-dashboards-new.yaml -n k8ssandra-operator
```

Access Grafana from http://localhost:3000, the credentials are admin/secret

```
kubectl port-forward svc/prometheus-grafana -n k8ssandra-operator 3000:80
```

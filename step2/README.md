# Community Over Code NA 2025 K8ssandra workshop
## Step 1 - Installation

k8ssandra-operator has a requirement that cert-manager is installed so that it can generate webhook certificates.

### Install cert-manager

```
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.18.2/cert-manager.yaml
```

Wait for the cert-manager pods to come up:

```
kubectl get pods -n cert-manager
```
```
NAME                                       READY   STATUS    RESTARTS   AGE
cert-manager-69f748766f-mk4h2              1/1     Running   0          37s
cert-manager-cainjector-7cf6557c49-29hb9   1/1     Running   0          37s
cert-manager-webhook-58f4cff74d-cdkzl      1/1     Running   0          37s
```

### Install k8ssandra-operator

```
kubectl apply -k "github.com/k8ssandra/k8ssandra-operator/config/deployments/control-plane/cluster-scope?ref=v1.26.0" --server-side
```

Wait for cass-operator and k8ssandra-operator to come up:

```
kubectl get pods -n k8ssandra-operator
```
```
NAME                                                READY   STATUS    RESTARTS   AGE
cass-operator-controller-manager-7c86cd444d-fmdsj   1/1     Running   0          36s
k8ssandra-operator-649fb8cd5-nq5wt                  1/1     Running   0          36s
```


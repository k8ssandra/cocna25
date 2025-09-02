# Community Over Code NA 2025 K8ssandra workshop
## Step 1 - Installation

k8ssandra-operator has a requirement that cert-manager is installed so that it can generate webhook certificates.

### Install cert-manager

Install cert-manager using Helm (recommended) or with kubectl

#### Using Helm

If using Helm v3.8.0 or newer:

```console
helm install \
  cert-manager oci://quay.io/jetstack/charts/cert-manager \
  --version v1.18.2 \
  --namespace cert-manager \
  --create-namespace \
  --set crds.enabled=true
```

For older versions:

```console
helm repo add jetstack https://charts.jetstack.io --force-update
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.18.2 \
  --set crds.enabled=true
```

#### Using kubectl

```console
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.18.2/cert-manager.yaml
```

#### Verifying installation

Wait for the cert-manager pods to come up:

```console
kubectl get pods -n cert-manager
```

```
NAME                                       READY   STATUS    RESTARTS   AGE
cert-manager-69f748766f-mk4h2              1/1     Running   0          37s
cert-manager-cainjector-7cf6557c49-29hb9   1/1     Running   0          37s
cert-manager-webhook-58f4cff74d-cdkzl      1/1     Running   0          37s
```

### Install k8ssandra-operator

Install k8ssandra-operator using Helm (recommended) or with kubectl (Kustomize template). 

#### Using Helm

```console
helm repo add k8ssandra https://helm.k8ssandra.io/stable
helm repo update
helm install k8ssandra-operator k8ssandra/k8ssandra-operator -n k8ssandra-operator --create-namespace
```

#### Using kubectl

```console
kubectl apply -k "github.com/k8ssandra/k8ssandra-operator/config/deployments/control-plane/cluster-scope?ref=v1.26.0" --server-side
```

#### Verifying installation

Wait for cass-operator and k8ssandra-operator to come up:

```
kubectl get pods -n k8ssandra-operator
```
```
NAME                                                READY   STATUS    RESTARTS   AGE
cass-operator-controller-manager-7c86cd444d-fmdsj   1/1     Running   0          36s
k8ssandra-operator-649fb8cd5-nq5wt                  1/1     Running   0          36s
```


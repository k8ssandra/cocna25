# Community Over Code NA 2025 K8ssandra workshop

## Prerequisites

Install either Kind (Kubernetes IN Docker) or Minikube (but we prefer Kind). You will also need kubectl and Helm is recommended.

### kubectl installation

If you don't have kubectl installed, follow the instructions:

[Install kubectl on macOS](https://kubernetes.io/docs/tasks/tools/install-kubectl-macos/)
[Install kubectl on Linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)
[Install kubectl on Windows](https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/)

## Kind installation

### Mac

```
brew install kind
```

### Windows


With chocolatey

```
choco install kind
```

With winget

```
winget install Kubernetes.kind
```

Powershell

```
curl.exe -Lo kind-windows-amd64.exe https://kind.sigs.k8s.io/dl/v0.29.0/kind-windows-amd64
Move-Item .\kind-windows-amd64.exe c:\some-dir-in-your-PATH\kind.exe
```

### Linux

#### For AMD64 / x86_64
```
[ $(uname -m) = x86_64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-$(uname)-amd64
```

#### For ARM64
```
[ $(uname -m) = aarch64 ] && curl -Lo ./kind https://kind.sigs.k8s.io/dl/v0.29.0/kind-$(uname)-arm64
chmod +x ./kind
sudo mv ./kind /usr/local/bin/kind
```

### If that doesn't work for you

Check the full instructions [here](https://github.com/kubernetes-sigs/kind?tab=readme-ov-file#installation-and-usage).

### Verify your installation

```
kind create cluster --name k8ssandra --config ./kind/w4k1.32.yaml
```

Which should output something such as:

```
Creating cluster "k8ssandra" ...
 ✓ Ensuring node image (kindest/node:v1.32.5) 🖼 
 ✓ Preparing nodes 📦 📦 📦 📦 📦  
 ✓ Writing configuration 📜 
 ✓ Starting control-plane 🕹️ 
 ✓ Installing CNI 🔌 
 ✓ Installing StorageClass 💾 
 ✓ Joining worker nodes 🚜 
Set kubectl context to "kind-k8ssandra"
You can now use your cluster with:

kubectl cluster-info --context kind-k8ssandra

Have a question, bug, or feature request? Let us know! https://kind.sigs.k8s.io/#community 🙂
```

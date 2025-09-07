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

### Pull the Cassandra docker images

```
docker pull k8ssandra/cass-management-api:5.0.3-ubi​
docker pull k8ssandra/cass-management-api:5.0.4-ubi
```

### Load the Cassandra images into the kind cluster

We will load the images we've pulled in the local docker daemon to the kind nodes, which will reduce the amount of times they get downloaded from the internet:

```
kind load docker-image k8ssandra/cass-management-api:5.0.3-ubi --name k8ssandra
kind load docker-image k8ssandra/cass-management-api:5.0.4-ubi --name k8ssandra
```

That should output something like this:

```
Image: "k8ssandra/cass-management-api:5.0.3-ubi" with ID "sha256:4971433fd4759caa5d0d151cd0145a0ac4c9b782662dde905a0621d3da1135b3" not yet present on node "k8ssandra-worker3", loading...
Image: "k8ssandra/cass-management-api:5.0.3-ubi" with ID "sha256:4971433fd4759caa5d0d151cd0145a0ac4c9b782662dde905a0621d3da1135b3" not yet present on node "k8ssandra-worker4", loading...
Image: "k8ssandra/cass-management-api:5.0.3-ubi" with ID "sha256:4971433fd4759caa5d0d151cd0145a0ac4c9b782662dde905a0621d3da1135b3" not yet present on node "k8ssandra-worker2", loading...
Image: "k8ssandra/cass-management-api:5.0.3-ubi" with ID "sha256:4971433fd4759caa5d0d151cd0145a0ac4c9b782662dde905a0621d3da1135b3" not yet present on node "k8ssandra-control-plane", loading...
Image: "k8ssandra/cass-management-api:5.0.3-ubi" with ID "sha256:4971433fd4759caa5d0d151cd0145a0ac4c9b782662dde905a0621d3da1135b3" not yet present on node "k8ssandra-worker", loading...
Image: "k8ssandra/cass-management-api:5.0.4-ubi" with ID "sha256:c518727d22763c748dc891c22df65fa158d9f32a212bcb65608963c4c970c57a" not yet present on node "k8ssandra-worker3", loading...
Image: "k8ssandra/cass-management-api:5.0.4-ubi" with ID "sha256:c518727d22763c748dc891c22df65fa158d9f32a212bcb65608963c4c970c57a" not yet present on node "k8ssandra-worker4", loading...
Image: "k8ssandra/cass-management-api:5.0.4-ubi" with ID "sha256:c518727d22763c748dc891c22df65fa158d9f32a212bcb65608963c4c970c57a" not yet present on node "k8ssandra-worker2", loading...
Image: "k8ssandra/cass-management-api:5.0.4-ubi" with ID "sha256:c518727d22763c748dc891c22df65fa158d9f32a212bcb65608963c4c970c57a" not yet present on node "k8ssandra-control-plane", loading...
Image: "k8ssandra/cass-management-api:5.0.4-ubi" with ID "sha256:c518727d22763c748dc891c22df65fa158d9f32a212bcb65608963c4c970c57a" not yet present on node "k8ssandra-worker", loading...
```
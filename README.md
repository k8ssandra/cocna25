# Community Over Code NA 2025 K8ssandra workshop

## Prerequisites

- A fully configured Docker installation (Docker Desktop, Colima, Podman, ...)
- [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/) (Kubernetes IN Docker).

## Kind installation

### Mac

```
brew install kind
```


### Windows

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

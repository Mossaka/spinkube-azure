# SpinKube Helm Chart

This is a Helm chart for deploying SpinKube on a Kubernetes cluster.

## Create new cluster

To create a new cluster, you can use the following command:

```bash
k3d cluster create wasm-cluster \
  --image ghcr.io/spinkube/containerd-shim-spin/k3d:v0.13.1 \
  --port "8081:80@loadbalancer" \
  --agents 2
```

## Install SpinKube
```bash
helm install spinkube ./spinkube --values ./spinkube/values.yaml
```
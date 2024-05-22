# SpinKube Helm Chart

This is a Helm chart for deploying SpinKube on AKS

## Create a new AKS cluster

To create a new AKS cluster, you can use the following command:

```bash
az login --use-device-code
export RG=spinkube-demo
az group create --name $(echo $RG) --location eastus2
az aks create --name spinkube-aks \
    --resource-group $(echo $RG) \
    --node-count 1 \
    --tier free \
    --generate-ssh-keys
az aks get-credentials --resource-group $(echo $RG) --name spinkube-aks
kubectl config current-context
```

## Install SpinKube
```bash
helm package .
helm install spinkube ./spinkube-demo-0.1.0.tgz

kubectl annotate node --all kwasm.sh/kwasm-node=true
kubectl apply -f spin-operator.shim-executor.yaml
```

## Deploy a Spin App
```bash
kubectl apply -f https://raw.githubusercontent.com/spinkube/spin-operator/main/config/samples/simple.yaml
```

and then check the status of the Spin App:
```bash
kubectl port-forward services/simple-spinapp 8080:80
```
```bash
curl http://localhost:8080/hello
```

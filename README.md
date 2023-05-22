# fluent-bit

https://docs.fluentbit.io/manual/

## Pre-requisite

```bash
kind create cluster --name kind-local
```

## Installation

```bash
mkdir -p ./install
cd install
kubectl create namespace logging

curl -fsSL -O https://raw.githubusercontent.com/fluent/fluent-bit-kubernetes-logging/master/fluent-bit-service-account.yaml && \
  kubectl create -f fluent-bit-service-account.yaml
curl -fsSL -O https://raw.githubusercontent.com/fluent/fluent-bit-kubernetes-logging/master/fluent-bit-role.yaml && \
  kubectl create -f fluent-bit-role.yaml
curl -fsSL -O https://raw.githubusercontent.com/fluent/fluent-bit-kubernetes-logging/master/fluent-bit-role-binding.yaml && \
  kubectl create -f fluent-bit-role-binding.yaml

# ConfigMap for our Fluent Bit DaemonSet
curl -fsSL -O https://raw.githubusercontent.com/fluent/fluent-bit-kubernetes-logging/master/output/elasticsearch/fluent-bit-configmap.yaml && \
  kubectl create -f fluent-bit-configmap.yaml
# Fluent Bit to Elasticsearch
curl -fsSL -O https://raw.githubusercontent.com/fluent/fluent-bit-kubernetes-logging/master/output/elasticsearch/fluent-bit-ds.yaml && \
  kubectl create -f fluent-bit-ds.yaml

cd ..
# kubectl delete -f ./install
```
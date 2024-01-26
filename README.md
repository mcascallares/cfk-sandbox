# CFK Sandox

This sample repo deploys Confluent Platform for Kubernetes (CFK) following the quickstart examples
of [this repo](https://github.com/confluentinc/confluent-kubernetes-examples/tree/master/quickstart-deploy).


## Requirements

  - Docker
  - [Kind](https://kind.sigs.k8s.io)
  - Helm 3 installed on your local machine
  - Kubectl installed on your local machine
  

## Deploy your Kubernetes cluster with Docker

Deploy your Kubernetes cluster, with 3 workers and 1 control plane nodes.

```
kind create cluster --config kind.yaml
```

Check that your kubernetes cluster is up and running

```
kubectl cluster-info --context kind-kind
```

## Namespacing CFK 

Create `confluent` namespace

```
kubectl create namespace confluent
```

Set it as current namespace

```
kubectl config set-context --current --namespace=confluent
```


## Set up the Helm Chart

```
helm repo add confluentinc https://packages.confluent.io/helm
```


## Install Confluent For Kubernetes using Helm

```
helm upgrade --install confluent-operator confluentinc/confluent-for-kubernetes --namespace confluent
```


## Deploy Confluent Platform

```
kubectl apply -f confluent-platform.yaml
```

## Validate in Control Center

Set up port forwarding to Control Center web UI from local machine:

```
kubectl port-forward controlcenter-0 9021:9021
```

Browse to Control Center in http://localhost:9021

## [Alternative] Deploy Confluent Platform - Minimal version

```
kubectl apply -f confluent-platform-minimal.yaml
```

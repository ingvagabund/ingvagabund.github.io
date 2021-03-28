---
layout: post
title:  "Testing descheduler with Kind"
date:   2021-03-28 12:43:45 +0100
categories: kubernetes
---

## Deploying testing cluster with Kind

With podman installed and descheduler project as the active directory, just run:

```
$ sudo kind create cluster --config=./hack/kind_config.yaml --image=docker.io/kindest/node:v1.20.2
enabling experimental podman provider
Creating cluster "kind" ...
podman provider does not work properly in rootless mode
[jchaloup@localhost descheduler]$ sudo kind create cluster --config=./hack/kind_config.yaml --image=docker.io/kindest/node:v1.20.2
[sudo] password for jchaloup:
enabling experimental podman provider
Creating cluster "kind" ...
 ✓ Ensuring node image (docker.io/kindest/node:v1.20.2) 🖼
 ✓ Preparing nodes 📦 📦 📦  
 ✓ Writing configuration 📜
 ✓ Starting control-plane 🕹️
 ✓ Installing CNI 🔌
 ✓ Installing StorageClass 💾
 ✓ Joining worker nodes 🚜
Set kubectl context to "kind-kind"
You can now use your cluster with:

kubectl cluster-info --context kind-kind

Have a question, bug, or feature request? Let us know! https://kind.sigs.k8s.io/#community 🙂
```

More about [Kind](https://kind.sigs.k8s.io/docs/user/quick-start/#creating-a-cluster)

Copy generated kubeconfig:

```
$ sudo cp /root/.kube/config ~/.kube/config
```

Check the cluster:

```
$ kubectl get nodes
NAME                 STATUS   ROLES                  AGE     VERSION
kind-control-plane   Ready    control-plane,master   5m12s   v1.20.2
kind-worker          Ready    <none>                 4m37s   v1.20.2
kind-worker2         Ready    <none>                 4m37s   v1.20.2
```

## Running descheduler e2e

```
$ sudo podman pull kubernetes/pause
$ sudo kind load docker-image docker.io/kubernetes/pause
```

To run a specific test (with klog logs):

```
$ go test sigs.k8s.io/descheduler/test/e2e -v -run TestLowNodeUtilization -args -v=1
```

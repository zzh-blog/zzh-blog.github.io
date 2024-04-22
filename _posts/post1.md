---
title: K8s学习记录
author: zzh
date: 2022-08-11 00:34:00 +0800
categories: [K8s, 笔记]
tags: [favicon]
---

安装minikube
```
brew install minikube
```


启动 minikube
```
minikube start
```

关闭 minikube
```
minikube stop
```

启动minikube dashboard
```cmd

minikube dashboard
```

默认情况下，Pod 只能通过 Kubernetes 集群中的内部 IP 地址访问。 要使得 hello-node 容器可以从 Kubernetes 虚拟网络的外部访问，你必须将 Pod 暴露为 Kubernetes Service.

在没有使用ingress时，如果想要访问服务，可以通过下面的方式

创建一个 deployment

```
kubectl create deployment hello-minikube --image=kicbase/echo-server:1.0
```

创建一个 node port的 service
kubectl expose deployment hello-minikube --type=NodePort --port=8080

将服务暴露出来
minikube service hello-minikube

使用ingress的方式

启用ingress插件
minikube addons enable ingress

开启通道
minikube tunnel

创建一个使用LoadBalancer方式的service
kubectl expose deployment hello-minikube --type=LoadBalancer --port=8080

查看服务的外部ip，然后通过外部ip+port就可以访问了
kubectl get svc hello-nginx

Kubectl的一些其他操作

持续显示pod中的第一个容器日志，类似于tail -f
kubectl logs -f hello-nginx

进入pod中的第一个容器
kubectl exec -ti hello-nginx — /bin/bash


获取services的信息，对于pod的操作类似
kubectl get services
获取单个service的信息
kubectl get services hello-nginx
描述某个服务的信息
kubectl describe services hello-nginx
删除某个service
kubectl delete services hello-nginx

开启对于kube的资源监测
minikube enable metric server

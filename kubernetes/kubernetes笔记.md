## 一、 Kubernetes基础

### 1. Kubernetes 由来

### 2. Kubernetes简介

### 3. Kubernetes架构

### 4. 安装及集群搭建

### 5. Pod基础与进阶

##### a. Pod定义与创建

##### b. 静态Pod 说明

##### c. Pod生命周期

##### e. Pod 的健康检查

##### f. 使用Capabilities



##  二、 深入理解Kubernetes

### 1. Kubernetes的设计理念

### 2. Kubernetes 的基础哲学

### 3. Kubernetes中常用的对象

##### a. 基础对象

* Namespace
* Pod
* Service
* Volume
  PV和PVC

##### b. 常用的Workloads Controller

* ReplicatSet
* Deployment
* StatefulSet
* DaemonSet
* Job
* 互相对比

##### c. 配置管理

* ConfigMap
* Secret

### 4. 服务发现与负载均衡

##### a. 集群内部服务发现
##### b. 集群外部访问服务
##### c. Headless Service
##### d. 自带DNS介绍
##### e. 4/7层服务发现

### 5. Kubernetes中的网络

##### a. 几种常见的通讯场景
##### b. CNI网络模型
##### c. 常用开源网络插件性能与比较

### 6. Kubernetes中的存储

##### a. 存储方案

##### b.常见的内置存储Plugin

### 7. 资源限制及Quota管理

### 8. 网络隔离

##### a. NetworkPolicy

### 9. CRI

## Kubernetes高阶实战

### 1. 三大核心组件原理分析

##### a. Kube-apiserver

* 认证
* 授权
  ABAC
  RBAC
  Webhook
  Node
* 准入控制

##### b. Kube-controller
##### c. kube-scheduler

* 亲和/反亲和
* Node Taints 和Tolerations
* Pod优先级与抢占
* PriorityClass
* Predict和Priority
* 多调度器

### 2. Kubernetes Garbage Collection 和 Pod驱逐

## Kubernetes落地实战

### 1. 微服务、Service Mesh和CI/CD的最佳实践

##### a. 部署
##### b. Brigade

### 2. Kubernetes Ingress

##### a. 什么是Ingress
##### b. Ingress Controller
##### c. NodePorts vs LB vs Ingress

### 3. Kubernetes Operator

##### a. Operator框架
##### b. 创建一个Operator
##### c. Operator的生命周期

### 4. Kubernetes集群灾备

##### a. 有状态vs无状态
##### b. Master/Node灾备
##### c. etcd灾备
##### d. PV灾备
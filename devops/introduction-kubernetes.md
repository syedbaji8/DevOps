# Introduction Kubernetes

<figure><img src="../.gitbook/assets/Introduction Kubernetes Mind Map.png" alt=""><figcaption></figcaption></figure>



{% embed url="https://www.coursera.org/learn/ibm-containers-docker-kubernetes-openshift/lecture/eHlCb/introduction-to-kubernetes" %}

## Learning Objectives

After watching this video, you will be able to:

1. Define Kubernetes.
2. Explain what Kubernetes is not.
3. Relate Kubernetes concepts.
4. Describe Kubernetes capabilities.
5. Describe the Kubernetes ecosystem.

## What Is Kubernetes?

The official Kubernetes documentation describes Kubernetes as:

> An open-source system for automating deployment, scaling, and management of containerized applications.

Kubernetes is an open-source containerization orchestration platform developed as a project by Google and currently maintained by the Cloud Native Computing Foundation.

It is widely available, portable across clouds and on premises, and recognized as the de facto choice for container orchestration.

Kubernetes as a service grew as an extension of containers as a service.

## Declarative Management

Kubernetes facilitates **declarative management**, in which it automatically performs the necessary operations toward achieving the called-for state.

```
Desired / called-for state
          ↓
     Kubernetes
          ↓
Automatically performs
necessary operations
          ↓
Achieves the called-for state
```

## What Kubernetes Is Not

Kubernetes is not:

* A traditional all-inclusive Platform as a Service.
* A rigid or opinionated platform.
* A platform limited to one workload style.
* A provider of continuous integration or continuous delivery pipelines to build applications or deploy source code.
* A system that prescribes logging, monitoring, or alerting solutions.
* A platform with built-in middleware, databases, or other services.

Kubernetes is a flexible model that supports an extremely diverse variety of workloads, including:

* Stateless workloads.
* Stateful workloads.
* Data processing workloads.
* Any application that can be containerized.

Organizations are free to select and integrate third-party and open-source tools.

## Kubernetes Concepts

Kubernetes concepts include:

* Pods and workloads.
* Services.
* Storage.
* Configuration.
* Security.
* Policies.
* Scheduling and eviction.
* Preemption.
* Cluster administration.

### Pods

Pods represent the smallest deployable compute object and the higher-level abstractions used to run workloads.

### Services

Services expose applications running on sets of Pods.

* Each Pod is assigned a unique IP address.
* Sets of Pods have a single DNS name.

```
Pods
 ├── Pod → unique IP
 ├── Pod → unique IP
 └── Pod → unique IP
        ↓
     Service
        ↓
Application exposure
```

### Storage

Kubernetes supports both persistent and temporary storage for Pods.

### Configuration

Configuration refers to the provisioning of resources for configuring Pods.

### Security

Security measures for cloud-native workloads enforce security for:

* Pod access.
* API access.

### Policies

Policies apply to groups of resources, ensuring that Pods match to nodes so that the kubelet can find and run them.

### Scheduling and Eviction

Scheduling and eviction run and proactively terminate one or more Pods on resource-starved Nodes.

```
Pod workload
    ↓
Scheduling
    ↓
Node placement
    ↓
Node becomes resource-starved
    ↓
Eviction
    ↓
One or more Pods may be proactively terminated
```

### Preemption

Preemption is about prioritization.

It terminates lower-priority Pods so that Pods with higher priority can schedule and run on Nodes.

```
Higher-priority Pod
        ↑
     Needs to run
        ↑
Preemption may terminate
lower-priority Pods
        ↓
Resources become available
        ↓
Higher-priority Pod schedules
```

### Cluster Administration

Cluster administration provides the details necessary to create or administer a cluster.

## Kubernetes Capabilities

Kubernetes capabilities include:

* Automated rollouts of changes to applications or configuration.
* Health monitoring and rolling back changes.
* Storage orchestration.
* Horizontal scaling of workloads based on metrics or via commands.
* Automated bin packing.
* Secret and configuration management.
* IPv4 and IPv6 addressing for Pods and services.
* Batch and continuous integration workload management.
* Self-healing and automatic replacement of failed containers.
* Service discovery.
* Load balancing.
* Extensibility without modifying source code.

### Automated Rollouts, Health Monitoring, and Rollback

Kubernetes can automate rollouts of changes to applications or configuration.

It also provides health monitoring and the ability to roll back changes.

### Storage Orchestration

Kubernetes mounts a chosen storage system, including:

* Local storage.
* Network storage.
* Public cloud storage.

### Horizontal Scaling

Kubernetes supports horizontal scaling of workloads based on metrics or via commands.

### Automated Bin Packing

Automated bin packing:

* Increases utilization.
* Creates cost savings.
* Uses a mix of critical and best-effort workloads.
* Performs container auto-placement based on resource requirements and conditions.
* Does not sacrifice high availability.

```
Workloads
   ↓
Resource requirements + conditions
   ↓
Automated container placement
   ↓
Better utilization
   ↓
Potential cost savings
   ↓
High availability maintained
```

### Secrets and Configuration Management

Kubernetes includes secret and configuration management for sensitive information, including:

* Passwords.
* OAuth tokens.
* SSH keys.

It handles deployments and updates to secrets and configuration without rebuilding images.

### IPv4 and IPv6 Support

Kubernetes assigns both IPv4 and IPv6 addresses to:

* Pods.
* Services.

### Batch and Continuous Integration Workloads

Kubernetes manages:

* Batch workloads.
* Continuous integration workloads.

### Self-Healing

Kubernetes automatically replaces failed containers and self-heals failing or unresponsive containers.

```
Container
   ↓
Failure or unresponsive state
   ↓
Kubernetes detects problem
   ↓
Failed container automatically replaced
   ↓
Workload continues
```

### Service Discovery and Load Balancing

Kubernetes discovers Pods using IP addresses or a DNS name.

It load balances traffic for better performance and high availability.

```
Incoming traffic
       ↓
Service discovery
       ↓
Load balancing
   ┌───┼───┐
   ↓   ↓   ↓
 Pod Pod Pod
```

### Extensibility

Kubernetes adds features to your cluster without modifying source code.

## Kubernetes Ecosystem

The Kubernetes ecosystem is large and rapidly growing, with widely available services, support, and tools.

Running containerized applications requires separate tools. In addition to the Kubernetes orchestration tool, the ecosystem includes services for:

* Building container images.
* Storing images in a container registry.
* Application logging.
* Application monitoring.
* CI/CD capabilities.

### Ecosystem Provider Categories

| Category               | Providers named in the lesson                                                    |
| ---------------------- | -------------------------------------------------------------------------------- |
| Public cloud           | Prisma, IBM, Google, AWS                                                         |
| Open source frameworks | Red Hat, VMware, SUS, Mesosphere, Docker, Cloud Foundry                          |
| Management             | Digital Ocean, loodse, SUPERGIANT, CloudSoft, turbonomic, Techtonic, Weaverworks |
| Tools                  | JFrog, Univa, Aspen Mesh, Bitnami, Cloud 66                                      |
| Monitoring and logging | sumologic, DATADOG, New Relic, iguazio, Grafana SignalFX, sysdig, Dynatrace      |
| Security               | GUARDCORE, BLACKDUCK, yubico, cilium, aqua, TwistLock, Alcide                    |
| Load balancing         | AVI networks, VMware, NGiNX                                                      |

```
                         Kubernetes Ecosystem
                                  |
        -------------------------------------------------
        |           |            |          |            |
   Cloud         Framework    Management   Tools     Operations
 Providers       Providers    Providers   Providers
        |           |            |          |
      IBM        Red Hat     Digital      JFrog
     Google      VMware      Ocean       Univa
      AWS        Docker      CloudSoft    Bitnami
      ...         ...          ...          ...
                                                     |
                                      -----------------------------
                                      |            |              |
                                 Monitoring     Security      Load Balancing
                                 & Logging      Providers       Providers
```

## Kubernetes at a Glance

### Definition

```
Open-source system for automating
deployment, scaling, and management
of containerized applications
```

### Core Concepts

```
Pods
Workloads
Services
Storage
Configuration
Security
Policies
Scheduling
Eviction
Preemption
Cluster Administration
```

### Core Capabilities

```
Automated Rollouts
Health Monitoring
Rollback
Storage Orchestration
Horizontal Scaling
Automated Bin Packing
Secrets Management
Configuration Management
IPv4 / IPv6
Batch + CI Workloads
Self-Healing
Service Discovery
Load Balancing
Extensibility
```

### Ecosystem Categories

```
Public Cloud
Open Source Frameworks
Management
Tools
Monitoring & Logging
Security
Load Balancing
```

## Lesson Summary

Kubernetes is a highly portable, horizontally scalable, open-source container orchestration system with automated deployment and simplified management capabilities.

Its concepts include:

* Pods and workloads.
* Services.
* Storage.
* Configuration.
* Security.
* Policies.
* Scheduling and eviction.
* Preemption.
* Administration.

Its capabilities include:

* Automated rollouts and rollbacks.
* Storage orchestration.
* Horizontal scaling.
* Automated bin packing.
* Secret and configuration management.
* IPv4/IPv6 dual-stack support.
* Batch execution.
* Self-healing.
* Service discovery.
* Load balancing.
* Extensibility.

Its ecosystem includes:

* Public cloud providers.
* Framework providers.
* Management providers.
* Tool providers.
* Monitoring and logging providers.
* Security providers.
* Load balancing providers.

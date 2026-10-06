# Container Orchestration

<figure><img src="../.gitbook/assets/Container Orchestration Mind Map.png" alt=""><figcaption></figcaption></figure>

## Learning Objectives

After watching this video, you will be able to:

1. Define the challenges of container management.
2. Determine when container orchestration is needed.
3. Demonstrate container orchestration benefits.

## Why Container Orchestration Is Needed

Everyone's container journey starts with one container. Over time, new applications are written and projects are deployed globally to increase availability. That one initial container inevitably becomes several containers.

Initially, that growth is easy to handle, but soon it becomes overwhelming. Connecting, managing, and scaling hundreds or thousands of containers for a large application, such as a database or web app, can easily get out of control.

To create scale and manage large numbers of containers, container orchestration is needed.

```
One container
    ↓
More applications and deployments
    ↓
Several containers
    ↓
Hundreds / thousands of containers
    ↓
Management complexity
    ↓
Container orchestration
```

## What Is Container Orchestration?

Container orchestration is a process that automates the container life cycle of a container-based or containerized application.

This includes:

* Deployment
* Management
* Scaling
* Networking
* Availability

Container orchestration is necessary in large dynamic environments because it:

* Streamlines complexity.
* Enables hands-off deployment and scaling.
* Increases speed, agility, and efficiency.
* Integrates into CI/CD workflows and DevOp practices.
* Allows development teams to use resources more efficiently.

It can be implemented on premises and in public, private, or multi-cloud environments.

Container orchestration is often a critical part of an organization's security, orchestration, automation, and response requirements, also known as SOAR requirements.

## Container Orchestration Features

Container orchestration tools have a wide variety of features.

| Feature                            | Description                                                                                           |
| ---------------------------------- | ----------------------------------------------------------------------------------------------------- |
| Application image definition       | Defines which container images make up the application, where they are located, and in what registry. |
| Provisioning and deployment        | Improves provisioning and deployment for a more automated, unified, and smooth process.               |
| Network security                   | Secures network connections between containers.                                                       |
| Availability and performance       | Relocates containers to another host if an outage or shortage of system resources occurs.             |
| Scaling and load balancing         | Scales containers to meet demand and load balances requests.                                          |
| Resource allocation and scheduling | Handles resource allocation and schedules containers to the underlying infrastructure.                |
| Rolling updates and rollbacks      | Performs rolling updates and rollbacks.                                                               |
| Health checks                      | Ensures applications are running or performs necessary actions when checks fail.                      |

## Configuration Files

Container orchestration uses configuration files written in:

```
YAML
JSON
```

These files configure each container so it can:

* Find resources.
* Establish a network.
* Store logs.

Container orchestration automatically schedules the deployment of a new container to a cluster and finds the right host based on predefined settings or restrictions.

```
New container
    ↓
Cluster deployment
    ↓
Evaluate predefined settings / restrictions
    ↓
Select the appropriate host
    ↓
Schedule container
```

It also manages the container life cycle based on specifications in the configuration file, including:

* System parameters, such as CPU and memory.
* File parameters, such as proximity and file metadata.

Container orchestration supports scaling and enhances productivity through automation.

## Container Orchestration Tools

| Tool             | Description                                                                                                                                      |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| Marathon         | A framework for Apache Mesos that automates much of container management and monitoring.                                                         |
| HachiCorps Nomad | A free and open source cluster management and scheduling tool supporting Docker and other workloads across operating systems and infrastructure. |
| Docker Swarm     | Automates deployment of containerized applications and is designed for Docker Engine and other Docker tools.                                     |
| Kubernetes       | An open source platform described as the defactor standard for container orchestration.                                                          |

> The source uses the terms “HachiCorps Nomad” and “defactor standard.”

### Marathon

Marathon is a framework for Apache Mesos, an open source cluster manager developed by the University of California at Berkeley.

It allows container infrastructure to scale by automating the bulk of:

* Management tasks.
* Monitoring tasks.

### HachiCorps Nomad

HachiCorps Nomad is a free and open source cluster management and scheduling tool that supports:

* Docker.
* Other stand-alone applications.
* Virtualized applications.
* Containerized applications.

It works on:

* All major operating systems.
* All infrastructure.
* On-premises environments.
* Cloud environments.

This flexibility lets teams work with any type and level of workload.

### Docker Swarm

Docker Swarm automates the deployment of containerized applications.

It was designed specifically to work with:

* Docker Engine.
* Other Docker tools.

This makes Docker Swarm a popular choice for teams already working in Docker environments.

### Kubernetes

Kubernetes was developed by Google and is maintained by the Cloud Native Computing Foundation, CNCF. It is described as the defactor standard for container orchestration.

Kubernetes automates container-management tasks including:

* Deployment.
* Storage provisioning.
* Load balancing.
* Scaling.
* Service discovery.
* Self-healing.

#### Self-healing

Self-healing is the ability to:

* Restart a failed container.
* Replace a failed container.
* Remove a failed container.

```
Failed container
      ↓
Self-healing
  ├── Restart
  ├── Replace
  └── Remove
```

Kubernetes has broad functionality and an expanding ecosystem of open source supporting tools. It is widely supported by leading cloud providers, many of whom offer fully managed Kubernetes services.

## Benefits of Container Orchestration

Container orchestration helps meet business goals and increase profitability through automation.

| Benefit                | Description                                                                                                                   |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------- |
| Increased productivity | Removes the burden of individually installing and managing each container.                                                    |
| Reduced errors         | Reduces errors by reducing the manual-management burden.                                                                      |
| Developer focus        | Frees development teams to focus on application improvement.                                                                  |
| Faster deployments     | Enables iterative release of new features and capabilities and rapid deployment of containers and containerized applications. |
| Reduced costs          | Service containers have lower overhead and use fewer resources than virtual machines or traditional servers.                  |
| Stronger security      | Shares resources and isolates application processes, improving overall container security.                                    |
| Easier scalability     | Supports scaling applications using a single command.                                                                         |
| Faster error recovery  | Detects and resolves issues, such as infrastructure failures, automatically.                                                  |
| Higher availability    | Automatic recovery helps maintain high availability.                                                                          |

```
Automation
   ↓
Less individual container installation and management
   ↓
Fewer errors
   ↓
More focus on application improvement
```

```
Infrastructure failure
        ↓
Automatic detection
        ↓
Automatic resolution
        ↓
High availability
```

## Summary

Managing large numbers of containers is difficult. Container orchestration automates the container life cycle, resulting in:

* Faster deployments.
* Reduced errors.
* Higher availability.
* Stronger security.

Popular container orchestration tools include Marathon, Nomad, Docker Swarm, and Kubernetes.

Container orchestration improves productivity, deployment, costs, security, scalability, and error recovery.

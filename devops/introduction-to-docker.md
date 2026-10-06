# Introduction to Docker

<figure><img src="../.gitbook/assets/Introduction to Docker Mind Map Concepts and Benefits.png" alt=""><figcaption></figcaption></figure>

## Learning Objectives

After watching this video, you will be able to:

1. Define what Docker is.
2. Describe the Docker process and underlying technology.
3. List the benefits of Docker containers.
4. Identify the challenges of Docker containers.

## What Docker Is

Available since **2013**, the official Docker definition, paraphrased, states that Docker is:

> **An open platform for developing, shipping, and running applications as containers.**

Docker became popular with developers because of its:

* Simple architecture
* Massive scalability
* Portability across multiple platforms, environments, and locations

Docker isolates applications from infrastructure, including:

| Infrastructure layer |
| -------------------- |
| Hardware             |
| Operating system     |
| Container runtime    |

## Docker Technology and Underlying Architecture

Docker is written in the **Go programming language** and uses **Linux kernel features** to deliver its functionality.

### Namespaces

Docker uses namespaces to provide an isolated workspace called the **container**.

{% stepper %}
{% step %}
### Create namespaces

Docker creates a set of namespaces for every container.
{% endstep %}

{% step %}
### Run aspects separately

Each aspect runs in a separate namespace.
{% endstep %}

{% step %}
### Limit access

Access is limited to that namespace.
{% endstep %}
{% endstepper %}

This namespace model provides the isolated workspace associated with a container.

## Docker Methodology and Related Innovations

Docker methodology has inspired additional innovations.

### Complementary Tools

| Tool               | Source context                                        |
| ------------------ | ----------------------------------------------------- |
| **Docker CLI**     | Complementary tool inspired by the Docker methodology |
| **Docker Compose** | Complementary tool inspired by the Docker methodology |
| **Prometheus**     | Complementary tool inspired by the Docker methodology |

### Plugins

The source also mentions various plugins, including:

* Storage plugins

### Orchestration Technologies

The source identifies orchestration technologies using:

* **Docker Swarm**
* **Kubernetes**

### Development Methodologies

The source identifies development methodologies using:

* **Microservices**
* **Serverless**

## Benefits of Docker

### Stable Application Deployments

Docker's consistent and isolated environments result in **stable application deployments**.

### Fast Deployments

Deployments occur in **seconds**.

### Faster Development

Docker images are:

* Small
* Reusable

Because of these characteristics, they significantly speed up the development process.

### Automation and Error Reduction

Docker automation capabilities help:

* Eliminate errors
* Simplify the maintenance cycle

### Agile and CICD DevOps Practices

Docker supports:

* Agile practices
* CICD DevOps practices

### Versioning

Docker's easy versioning speeds up:

* Testing
* Rollbacks
* Redeployments

### Application Segmentation

Docker helps segment applications for easy:

* Refresh
* Cleanup
* Repair

### Collaboration and Issue Resolution

Developers collaborate to:

* Resolve issues faster
* Scale containers when needed

### Portability

Docker images are **platform independent**, so they are highly portable.

## Benefits Summary

| Benefit area           | Detail stated in the source                                                   |
| ---------------------- | ----------------------------------------------------------------------------- |
| Application stability  | Consistent and isolated environments result in stable application deployments |
| Deployment speed       | Deployments occur in seconds                                                  |
| Development speed      | Small, reusable images significantly speed up development                     |
| Automation             | Automation capabilities help eliminate errors                                 |
| Maintenance            | Automation simplifies the maintenance cycle                                   |
| DevOps                 | Supports Agile and CICD DevOps practices                                      |
| Versioning             | Speeds up testing, rollbacks, and redeployments                               |
| Application management | Enables easy refresh, cleanup, and repair through application segmentation    |
| Collaboration          | Developers collaborate to resolve issues faster                               |
| Scaling                | Developers can scale containers when needed                                   |
| Portability            | Platform-independent images are highly portable                               |

## Docker Capabilities and Concepts

| Concept                     | Details                                                                        |
| --------------------------- | ------------------------------------------------------------------------------ |
| Open platform               | Used for developing, shipping, and running applications as containers          |
| Simple architecture         | One reason given for Docker's popularity                                       |
| Scalability                 | Docker is described as having massive scalability                              |
| Portability                 | Works across multiple platforms, environments, and locations                   |
| Infrastructure isolation    | Isolates applications from hardware, operating system, and container runtime   |
| Go                          | Programming language Docker is written in                                      |
| Linux kernel features       | Used to deliver Docker functionality                                           |
| Namespaces                  | Provide an isolated workspace called the container                             |
| Per-container namespaces    | Docker creates a set of namespaces for every container                         |
| Namespace isolation         | Each aspect runs in a separate namespace with access limited to that namespace |
| Small images                | Help speed development                                                         |
| Reusable images             | Help speed development                                                         |
| Automation                  | Helps eliminate errors and simplify maintenance                                |
| Versioning                  | Speeds testing, rollbacks, and redeployments                                   |
| Application segmentation    | Enables easier refresh, cleanup, and repair                                    |
| Platform-independent images | Provide high portability                                                       |

## Docker Ecosystem

| Category                  | Items                      |
| ------------------------- | -------------------------- |
| Docker tools              | Docker CLI, Docker Compose |
| Monitoring/tooling        | Prometheus                 |
| Plugins                   | Storage plugins            |
| Orchestration             | Docker Swarm, Kubernetes   |
| Development methodologies | Microservices, Serverless  |

## Commands and Code

The supplied source does not contain any executable Docker commands, shell commands, Dockerfiles, configuration snippets, or code examples.

The following names are mentioned in the source, but they are technologies or tools rather than command examples:

* Docker CLI
* Docker Compose
* Prometheus
* Docker Swarm
* Kubernetes

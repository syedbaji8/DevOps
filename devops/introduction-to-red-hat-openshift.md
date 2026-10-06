# Introduction to Red Hat OpenShift

<figure><img src="../.gitbook/assets/OpenShift Study Guide Infographic.png" alt=""><figcaption></figcaption></figure>

## Overview

**OpenShift**, developed and supported by **Red Hat**, is an **enterprise-ready Kubernetes container platform built for the hybrid Cloud strategy**.

It provides a consistent application platform for managing:

* Hybrid deployments
* Multi-Cloud deployments
* Edge deployments

OpenShift is built on:

* Linux
* Containers
* Automation

It provides:

* Full-stack automated operations
* Self-service provisioning for developers
* A way for developers to efficiently move ideas from development to production

_Source-grounded overview of OpenShift definition, features, Kubernetes relationship, architecture, components, CLI, and enterprise capabilities._

## Learning Objectives

After watching this video, the learner will be able to:

1. Explain what OpenShift is and list its features.
2. Describe OpenShift CLI, architecture, and components.
3. Compare OpenShift with Kubernetes.

## OpenShift Foundation and Lifecycle

Besides container orchestration, OpenShift provides additional tooling around the complete application lifecycle:

```
Build
  ↓
CI/CD
  ↓
Monitoring
  ↓
Logs
```

OpenShift is not limited to orchestration; it adds tooling around the broader application life cycle.

## OpenShift Features

### Scale

Applications can scale to:

* **Thousands of instances**
* Across **hundreds of nodes**
* In **seconds**

### Hybrid Infrastructure

Flexible hybrid infrastructure options simplify:

* Deployment
* Management

### Open Standards

OpenShift uses open-source standards including:

* Kubernetes
* **Open Container Initiative (OCI)** containers

This supports familiar development practices and portable containers across multiple environments.

### Developer Tools

OpenShift includes a comprehensive set of developer tools, including:

* Multi-language support
* Command-line tools
* IDE integrations
* Other developer tooling

### Automated Upgrades and OperatorHub

OpenShift supports:

* Over-the-air platform upgrades
* Services from **OperatorHub**

OperatorHub services can be fully configured and deployed with one-click upgrades.

### Automation and Streamlining

OpenShift streamlines and automates:

* Container builds
* Application builds
* Deployments
* Scaling
* Health management

### Edge Architecture

OpenShift enhances support for smaller-footprint topologies in edge scenarios, with emphasis on:

* Mapping
* Connectivity
* Availability

### Multi-Cluster Management

OpenShift can manage and enforce policies across multiple clusters at scale.

### Security and Compliance

Capabilities include:

* Access controls
* Networking
* Enterprise registry
* Built-in scanner
* Enhanced threat detection
* Life-cycle vulnerability management
* Risk profiling

### Persistent Storage

OpenShift supports enterprise persistent storage solutions for:

* Stateful applications
* Stateless applications

### Partner Ecosystem

The OpenShift partner ecosystem adds:

* Storage services
* Network services
* IDE integrations
* CI integrations
* Other services and integrations

### Feature Labels

| Feature label                  |
| ------------------------------ |
| Scalable                       |
| Flexible                       |
| Open source                    |
| Portable containers            |
| Enhanced developer experience  |
| Automated installs & upgrades  |
| Automation & streamlining      |
| Edge architecture support      |
| Multi cluster management       |
| Advanced security & compliance |
| Persistent storage             |

## OpenShift and Kubernetes

Both Kubernetes and OpenShift are container orchestration platforms.

* Kubernetes is a critical component of OpenShift.
* OpenShift is an extension of Kubernetes.
* OpenShift provides a more robust and comprehensive platform for containerized applications.

```
Kubernetes
    ↓
OpenShift extension
    ↓
Broader platform capabilities for containerized applications
```

## OpenShift vs Kubernetes

| Aspect           | OpenShift                                        | Kubernetes                                |
| ---------------- | ------------------------------------------------ | ----------------------------------------- |
| Type             | Product                                          | Open-source project                       |
| Installation     | Limited options after installation starts        | All Linux environments                    |
| Flexibility      | Less flexible / some limitations                 | More flexible                             |
| Platforms        | Online, Azure, and dedicated                     | EKS (AWS), GKE (GCP), AKS (Azure)         |
| Image management | Image streams provide better management          | Container image management is not as easy |
| Security         | Very strict policy / “Not easy” in slide summary | Security maintenance is easy              |
| Router / Ingress | Router objects permit external access            | Ingress objects permit external access    |
| Deployment       | Less flexible deployment config command          | More flexible deployment objects          |
| UX               | Good UX / easy for beginners                     | Extra tools / harder for beginners        |
| Networking       | Good solutions out of the box                    | Third-party plugins when needed           |
| Services         | Good service catalog                             | Limited provision                         |
| Learning         | Easy for beginners                               | Hard for beginners                        |
| CI/CD            | Integrates with Jenkins                          | Integrates, but not with Jenkins          |

{% hint style="info" %}
The transcript and visual comparison slide use slightly different shorthand in a few places, such as “Very strict security policy” versus “Not easy.” These are different phrasings of the same source comparison.
{% endhint %}

## OpenShift Platform Architecture

OpenShift runs on top of a Kubernetes cluster.

* Object data is stored in the **`etcd` key-value store**.
* OpenShift has a **microservices-based architecture**.
* Its services are **REST APIs**.
* REST APIs expose the core objects.
* Controllers read the REST APIs.
* Controllers apply changes to other objects.
* Controllers report status or write back to the object.
* Controllers maintain the cluster desired state.

```
OpenShift
   ↓
Kubernetes cluster
   ↓
REST APIs → expose core objects
   ↓
Controllers → read APIs / apply changes / report status
   ↓
Cluster desired state

Object data → etcd key-value store
```

## Docker, Kubernetes, and OpenShift Roles

| Technology | Role described by the source                                                                                                                                       |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Docker     | Provides abstraction for packaging and creating Linux-based lightweight container images                                                                           |
| Kubernetes | Provides cluster management and orchestrates containers on multiple hosts                                                                                          |
| OpenShift  | Adds source-code management, builds, deployments, image management/promotion at scale, application management, team/user management, and networking infrastructure |

OpenShift adds:

* Management of source code
* Builds
* Deployments for developers
* Managing and promoting images at scale as they flow through the system
* Application management at scale
* Team and user tracking and management for a large developer organization
* Networking infrastructure supporting the cluster

## OpenShift Components

### Red Hat Base Layer

In an OpenShift environment:

* The Kubernetes master runs on **Red Hat Enterprise Linux CoreOS**.
* Worker nodes support **Red Hat Enterprise Linux**.

This is the **Red Hat base layer**.

### Kubernetes Layer

Above the Red Hat base layer are:

* Kubernetes architecture
* A set of services

### Service Categories

| Service category     | Purpose described in the source    |
| -------------------- | ---------------------------------- |
| Cluster services     | Cluster-level capabilities         |
| Platform services    | Help users manage workloads        |
| Application services | Help users build cloud-native apps |
| Developer services   | Increase developer productivity    |

### Cluster Services

Examples include:

* Integrated monitoring
* Private registry within the cluster
* Networking solutions
* Other cluster services

```
Cluster services | Platform services | Application services | Developer services
                              ↓
                         Kubernetes
                              ↓
Red Hat Enterprise Linux & Red Hat Enterprise Linux CoreOS
```

## OpenShift CLI

OpenShift offers CLI tools that let users perform administrative and development operations from the terminal.

### `oc`

**`oc`** is the most commonly used OpenShift CLI tool for end-to-end operations.

It runs on:

* Windows
* Linux
* Mac

It lets users:

* Work directly with project source code
* Script OpenShift operations
* Manage projects when bandwidth is restricted
* Manage projects when the web console is unavailable

{% hint style="warning" %}
The transcript contains the awkward phrase “using command script, script OpenShift operations.” The surrounding explanation supports the interpretation that `oc` can work with source code and script OpenShift operations, but the exact wording is transcription-unclear.
{% endhint %}

## `oc` and `kubectl`

Because OpenShift runs on top of Kubernetes, a copy of **`kubectl`** is included with `oc`.

* `oc` and `kubectl` binaries offer the same capabilities.
* `oc` is further extended to natively support OpenShift-specific features.

```
kubectl
  ↓
Kubernetes capabilities

oc
  ↓
Kubernetes capabilities
  +
OpenShift-specific capabilities
```

### OpenShift-Specific Features

* DeploymentConfigs
* BuildConfigs
* Routes
* ImageStreams
* ImageStreamTags

These features are not available in standard Kubernetes.

## OpenShift-Specific CLI Capabilities

### Authentication

`oc` provides an in-built login command for authentication.

### Application Startup

Additional commands such as **new app** are supported by `oc`.

This makes it easier to get new applications started using:

* Existing source code
* Pre-built images

{% hint style="warning" %}
The source uses the phrase “commands like new app” and does not provide the full command syntax or flags.
{% endhint %}

## Application, Image, Team, and User Management

OpenShift adds developer and organizational capabilities beyond basic container orchestration:

* Source-code management
* Builds
* Deployments
* Image management at scale
* Image promotion at scale as images flow through the system
* Application management at scale
* Team tracking
* User tracking
* Management of a large developer organization
* Networking infrastructure supporting the cluster

## Deployment Environments and Infrastructure

OpenShift is designed for a hybrid Cloud strategy and can consistently manage:

* Hybrid deployments
* Multi-Cloud deployments
* Edge deployments

The comparison also references:

* Online OpenShift availability
* Azure
* Dedicated OpenShift environments
* AWS EKS
* GCP GKE
* Azure AKS

Flexible hybrid infrastructure options simplify deployment and management.

## Security, Networking, Storage, and Partner Ecosystem

### Security

OpenShift provides or supports:

* Access controls
* Enterprise registry
* Built-in scanner
* Enhanced threat detection
* Life-cycle vulnerability management
* Risk profiling
* Networking
* Policy management across multiple clusters

### Networking

The source describes:

* Good networking solutions out of the box
* Networking infrastructure supporting the cluster
* Edge mapping, connectivity, and availability support

### Storage

OpenShift supports enterprise persistent storage for:

* Stateful apps
* Stateless apps

### Partner Ecosystem

The OpenShift partner ecosystem provides additional:

* Storage services
* Network services
* IDE integrations
* CI integrations
* Other services

## Video Visual Context

### What You Will Learn

_Source: video, \~00:20. Shows the lesson's learning-objective slide and its visual organization._

### What Is Red Hat OpenShift?

_Source: video, \~01:00. Shows the definition and four visual supporting statements: consistent platform for hybrid/multi-cloud/edge, Linux/containers/automation foundation, full-stack automation/self-service provisioning, and application lifecycle tooling._

### OpenShift Features

_Source: video, \~02:20. Shows the feature-label grid used in the lesson._

### OpenShift vs Kubernetes

_Source: video, \~03:00. Shows the first portion of the comparison table: type, installation, flexibility, platforms, management, and security._

_Source: video, \~03:40. Shows router/ingress, deployment, UX, networking, services, learning, and CI/CD comparison rows._

### OpenShift Platform Architecture

_Source: video, \~05:00. Shows the architecture statement that OpenShift runs on Kubernetes, stores object data in `etcd`, uses a microservices-based architecture, and the Docker abstraction note._

### OpenShift Components

_Source: video, \~05:40. Shows the component/service stack: cluster services, platform services, application services, developer services, Kubernetes, and the Red Hat Enterprise Linux / Red Hat Enterprise Linux CoreOS base layer._

### OpenShift CLI

_Source: video, \~06:20. Shows the CLI overview and identifies `oc` as the common end-to-end OpenShift CLI across Windows, Linux, and Mac._

### Why Use `oc` Over `kubectl`?

_Source: video, \~07:00. Shows that `oc` includes `kubectl` capabilities and adds DeploymentConfigs, BuildConfigs, Routes, ImageStreams, and ImageStreamTags._

### Recap

_Source: video, \~07:30. Shows the final recap that Kubernetes and OpenShift are container orchestration platforms and that OpenShift is an enterprise-ready Kubernetes container platform built for open hybrid cloud._

## Key Terms

| Term                            | Definition / meaning supported by the source                                                                       |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| **OpenShift**                   | Enterprise-ready Kubernetes container platform built for the hybrid Cloud strategy                                 |
| **Kubernetes**                  | Container orchestration platform and critical component of OpenShift                                               |
| **Container orchestration**     | Platform capability used by Kubernetes and OpenShift to orchestrate containers                                     |
| **Hybrid Cloud**                | Deployment strategy supported by OpenShift                                                                         |
| **Multi-Cloud**                 | Managing deployments across multiple cloud environments                                                            |
| **Edge deployment**             | Smaller-footprint/edge deployment scenario supported by OpenShift                                                  |
| **OCI**                         | Open Container Initiative; the source references OCI containers                                                    |
| **OperatorHub**                 | Source of services that can be configured and deployed with one-click upgrades                                     |
| **ImageStream**                 | OpenShift image-management capability                                                                              |
| **ImageStreamTag**              | OpenShift feature for image-stream tags                                                                            |
| **DeploymentConfig**            | OpenShift-specific deployment capability supported by `oc`                                                         |
| **BuildConfig**                 | OpenShift-specific build capability supported by `oc`                                                              |
| **Route**                       | OpenShift object used to permit external access                                                                    |
| **Ingress**                     | Kubernetes object used to permit external access to Kubernetes clusters                                            |
| **`etcd`**                      | Key-value store where OpenShift object data is stored                                                              |
| **REST API**                    | Service interface exposing core OpenShift objects                                                                  |
| **Controller**                  | Component that reads REST APIs, applies object changes, reports status or writes back, and maintains desired state |
| **Microservices architecture**  | Architecture model stated for OpenShift                                                                            |
| **`oc`**                        | OpenShift CLI used for end-to-end administration and development operations                                        |
| **`kubectl`**                   | Kubernetes CLI binary included with `oc`                                                                           |
| **Cluster services**            | Cluster-level services shown in the OpenShift component layers                                                     |
| **Platform services**           | Services that help users manage workloads                                                                          |
| **Application services**        | Services that help users build cloud-native applications                                                           |
| **Developer services**          | Services intended to increase developer productivity                                                               |
| **Enterprise registry**         | Registry capability included among OpenShift security/platform capabilities                                        |
| **Persistent storage**          | Enterprise storage capability for stateful and stateless applications                                              |
| **OpenShift partner ecosystem** | Ecosystem providing additional storage, network, IDE, CI, and other services and integrations                      |

## Command Reference

The source names CLI tools and command names but does not supply complete flags, arguments, or full invocation syntax.

### OpenShift CLI Tools

| Command / Tool | Purpose                                                        | Syntax / Example      | Notes                                                              |
| -------------- | -------------------------------------------------------------- | --------------------- | ------------------------------------------------------------------ |
| `oc`           | End-to-end OpenShift administrative and development operations | `bash<br>oc<br>`      | Most commonly used OpenShift CLI; complete invocation not supplied |
| `kubectl`      | Kubernetes CLI capability                                      | `bash<br>kubectl<br>` | A copy is included with `oc`                                       |

### Commands Mentioned by Name

| Command   | Purpose                                                           | Syntax / Example      | Notes                                                                          |
| --------- | ----------------------------------------------------------------- | --------------------- | ------------------------------------------------------------------------------ |
| `login`   | Authentication                                                    | `bash<br>login<br>`   | Source says `oc` has an in-built login command; exact full syntax not supplied |
| `new app` | Start applications using existing source code or pre-built images | `bash<br>new app<br>` | Source says “commands like new app”; full syntax and flags not supplied        |

{% hint style="warning" %}
The source gives only command names in these cases. It does not provide the full `oc` command syntax, flags, authentication parameters, or application arguments.
{% endhint %}

### OpenShift-Specific Capabilities

These are feature and object names, not complete command examples:

```
DeploymentConfigs
BuildConfigs
Routes
ImageStreams
ImageStreamTags
```

`oc` natively supports these capabilities, which are not available in standard Kubernetes.

## Source Notes

### Transcript Agreement

The supplied TXT and VTT contain the same spoken lesson content after whitespace normalization. The VTT contributes timestamp metadata but no separate spoken topic.

### Ambiguous or Unclear Items

{% hint style="warning" %}
The phrase surrounding `oc` and “command script, script OpenShift operations” is awkwardly transcribed. The surrounding material supports the general meaning that `oc` can work with source code and script OpenShift operations, but the exact sentence is unclear.
{% endhint %}

{% hint style="warning" %}
The availability phrase “online with Azure and dedicated” is preserved because the source does not further define the dedicated option.
{% endhint %}

{% hint style="warning" %}
The transcript says “Kubernetes security maintenance is easy” while the visual comparison summarizes the Kubernetes security cell as “Easy.” These are source statements, not independently verified claims.
{% endhint %}

{% hint style="warning" %}
The phrase “less provision for better services in clusters” is preserved as the source wording; the lesson does not further explain what “less provision” means.
{% endhint %}

{% hint style="warning" %}
`new app` is mentioned as a command name, but the lesson does not supply the full invocation or flags.
{% endhint %}

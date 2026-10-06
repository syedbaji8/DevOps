# Operators

<figure><img src="../.gitbook/assets/OpenShift Operators Mind Map.png" alt=""><figcaption></figcaption></figure>

## Overview

This lesson explains **Kubernetes Operators**: what an Operator is, how Operators extend the Kubernetes API and automate cluster tasks, how **Custom Resource Definitions (CRDs)** work with **custom controllers** to create the **Operator Pattern**, and how the **Operate Framework**, **Operator Hub**, and **Operator Maturity Model** support building and managing Operators. It also compares Operators with Service Brokers and gives practical examples and a step-by-step application deployment pattern.

## Table of Contents

* [Source Coverage and Reconciliation](operators.md#source-coverage-and-reconciliation)
* [Learning Objectives](operators.md#learning-objectives)
* [What Is an Operator](operators.md#what-is-an-operator)
* [Why Use Operators](operators.md#why-use-operators)
* [Human Operators vs Software Operators](operators.md#human-operators-vs-software-operators)
* [Operators vs Service Brokers](operators.md#operators-vs-service-brokers)
* [Custom Resource Definitions (CRDs)](operators.md#custom-resource-definitions-crds)
* [Custom Controllers](operators.md#custom-controllers)
* [The Operator Pattern](operators.md#the-operator-pattern)
* [Operator Framework](operators.md#operator-framework)
* [Operator SDK](operators.md#operator-sdk)
* [Operator Lifecycle Manager (OLM)](operators.md#operator-lifecycle-manager-olm)
* [Operator Registry](operators.md#operator-registry)
* [Operator Hub](operators.md#operator-hub)
* [Operator Maturity Model](operators.md#operator-maturity-model)
* [Operator Examples](operators.md#operator-examples)
* [Operators in Practice](operators.md#operators-in-practice)
* [Operator Deployment and Reconciliation Flow](operators.md#operator-deployment-and-reconciliation-flow)
* [Benefits and Capabilities Reference](operators.md#benefits-and-capabilities-reference)
* [Command Reference](operators.md#command-reference)
* [Video Visual Context](operators.md#video-visual-context)
* [Key Terms / Glossary](operators.md#key-terms--glossary)
* [Complete Lesson Walkthrough](operators.md#complete-lesson-walkthrough)
* [Source Notes](operators.md#source-notes)

## Source Coverage and Reconciliation

| Source                       | Details                                                  |
| ---------------------------- | -------------------------------------------------------- |
| `Operators.txt`              | Complete continuous transcript supplied with the lesson  |
| `Operators-subtitles-en.vtt` | 116 timestamped subtitle cues                            |
| `Operators.mp4`              | Original video, inspected for slide-level visual context |
| TXT/VTT comparison           | **Exact match after whitespace normalization**           |
| Video duration               | Approximately **381.47 seconds** (6:21)                  |

The TXT and VTT contain the same spoken content. The VTT adds timing segmentation but no additional spoken material, so the transcript is consolidated once in the body instead of duplicated.

The video was inspected at representative points to capture visual slide content that supplements the spoken narration, including the Operator introduction diagram, Service Brokers vs Operators table, CRD and custom-controller diagrams, Operator Framework, Maturity Model, practice flow, OperatorHub, and recap.

> **Source-fidelity rule:** Source terminology and framing are retained. No outside technical correction is silently substituted. Where the visual slide contains detail that is not fully spoken, it is identified as visual-only or flagged as unclear rather than inferred beyond what can be observed.

## Learning Objectives

After watching the video, the learner will be able to:

1. Define an Operator and explain its purpose.
2. Show the relation between:
   * Custom controllers.
   * The Operator Pattern.
   * Custom Resource Definitions (CRDs).
3. Explain the purpose of:
   * Operator Hub.
   * Operator Framework.
   * Operator Maturity Model.

## What Is an Operator

The lesson defines Operators as software that:

* Automate cluster tasks.
* Act as a custom controller to extend the Kubernetes API.
* Run in a pod.
* Interact with the API server.
* Package, deploy, and manage Kubernetes applications.
* Automate application creation, configuration, and management through continuous, real-time decisions.

The lesson also states that Operators:

* Package native applications for Kubernetes.
* Deploy native applications in Kubernetes.
* Manage native applications in Kubernetes.
* Automate other tasks.
* Ensure all relevant components are included.

### Operator Introduction Diagram

The video visually represents an Operator running in a pod and interacting with Kubernetes.

The diagram shows a relationship among:

```
Custom Resource
      ↓
    watches
      ↓
   Operator
      ↓
 Kubernetes API
      ↓
 adjust state
```

The diagram also shows users modifying the custom resource and change events moving through the Operator.

_Source: video, approximately 00:35. The frame shows the Operator as a controller running in a pod and interacting with the Kubernetes API through a watched custom resource._

## Why Use Operators

The lesson identifies these Operator capabilities:

1. Repeatable installs and upgrades.
2. Regular full-system health checks.
3. Over-the-air (OTA) updates.
4. A way to collect and spread knowledge from field engineers to all users.
5. Integration with APIs and CLI tools such as `kubectl` and `OC` commands.

### Why-Use-Operators Visual

_Source: video, approximately 01:35. The slide visually groups repeatable installs and upgrades, regular full-system health checks, over-the-air updates, communication tools, and integration._

## Human Operators vs Software Operators

The lesson distinguishes two kinds of Operators:

| Type                   | Description                                                                                    |
| ---------------------- | ---------------------------------------------------------------------------------------------- |
| **Human operators**    | Understand the system they control; know how to deploy services and recognize and fix problems |
| **Software operators** | Try to capture the knowledge of human operators and automate the same processes                |

This creates the core idea of the Operator pattern:

```
Human operational knowledge
          ↓
Captured as software logic
          ↓
Automated operational behavior
```

## Operators vs Service Brokers

The lesson compares Service Brokers and Operators.

### Comparison

| Aspect                           | Service Brokers provide                                                          | Operators provide                                                       |
| -------------------------------- | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Process duration                 | Short-running process                                                            | Long-running process                                                    |
| Daily operations                 | Cannot perform consecutive-day operations such as upgrades, failover, or scaling | Can perform operations such as upgrades, failover, or scaling every day |
| Customization / parameterization | Only at the time of installation                                                 | Operators constantly watch current cluster state                        |
| Off-cluster services             | Supported                                                                        | Supported                                                               |

The source specifically uses the examples:

```
Upgrades
Failover
Scaling
```

for operations that Operators can perform continuously and Service Brokers cannot perform as ongoing daily operations.

### Visual Comparison

_Source: video, approximately 01:55–02:15. The visual table compares short-running Service Broker processes with long-running Operator processes, including customization and parameterization._

> ⚠️ **Unclear in source:** The narration says Service Brokers provide “off-cluster services” and then also lists “off-cluster services” under Operators. This is retained exactly as a source statement rather than reconciled using outside knowledge.

## Custom Resource Definitions (CRDs)

A **Custom Resource Definition (CRD)**:

* Stores and retrieves objects in the Kubernetes API.
* Extends the Kubernetes API beyond built-in resources such as Deployments and Pods.
* Makes the Kubernetes API more modular and flexible.
* Can be installed by users into clusters.

The source states an important scope characteristic:

* Each CRD is available only in the cluster where it is installed.

Once installed:

* CRD objects are accessible using `kubectl`.
* They can be accessed similarly to Pods and other Kubernetes resources.

### CRD Visual

_Source: video, approximately 02:35. The slide states that CRDs store and retrieve objects in the Kubernetes API, extend the API, make it more modular/flexible, and can be installed in clusters._

## Custom Controllers

To change the state of a cluster, **custom controllers** are used.

Controllers:

* Reconcile a cluster's actual state with its configured state.

Custom controllers do the same type of reconciliation for:

* Custom resources.

### Custom Controller Visual

The video shows a Kubernetes cluster containing:

* A CRD.
* A Controller (Operator Pod).
* Other objects such as StatefulSet, ConfigMap, Service, and Pods.

The diagram visually shows the Controller:

* Monitoring the CRD.
* Reconciling resources.
* Keeping the actual state aligned with the desired state.

_Source: video, approximately 03:15. The slide shows a CRD, controller/operator pod, resource objects, and reconciliation inside a Kubernetes cluster._

## The Operator Pattern

The lesson states that:

* Combining CRDs and custom controllers creates a **declarative API**.
* This combination is known as the **Operator Pattern**.

Custom controllers interpret:

* CRD data as the desired state.

They then:

* Reconcile the cluster's actual state so that it matches the CRD data.

### Operator Pattern Flow

```
CRD
 ↓
Desired State
 ↓
Custom Controller
 ↓
Reconcile
 ↓
Actual Cluster State
 ↓
Match Desired State
```

### Key Relationship

```
CRD + Custom Controller
          ↓
   Declarative API
          ↓
   Operator Pattern
```

This is the central conceptual relationship in the lesson.

## Operator Framework

The **Operator Framework** is described as an open-source toolset covering:

* Coding.
* Testing.
* Delivery.
* Operator updates.

The video shows the framework as three principal components:

```
Operator SDK
       +
Operator Lifecycle Manager (OLM)
       +
Operator Registry
```

_Source: video, approximately 03:35. The slide introduces the Operator Framework and its components._

## Operator SDK

The **Operator SDK** is part of the Operator Framework.

The lesson states that the SDK includes:

* Helm.
* Go.
* Ansible.

The Operator SDK helps authors:

* Build Operators.
* Test Operators.
* Package Operators.

It does this without requiring authors to know the complexities of the Kubernetes API.

## Operator Lifecycle Manager (OLM)

The **Operator Lifecycle Manager (OLM)**:

* Controls Operator installation.
* Controls Operator upgrades.
* Controls role-based access control (RBAC) of Operators in a cluster.

In the Operator Framework visual, OLM is shown as responsible for:

```
Install
Upgrade
RBAC
```

## Operator Registry

The **Operator Registry** stores:

* CRDs.
* Cluster Service Versions (CSVs).
* Operator metadata.

The stored information is associated with:

* Packages.
* Channels.

The Registry:

* Runs in Kubernetes or OpenShift clusters.
* Provides Operator catalog data to OLM.

## Operator Hub

The **Operator Hub** is a web console.

It allows cluster administrators to:

* Find Operators.
* Install Operators on their cluster.

The video shows OperatorHub as a graphical catalog from which Operators can be installed.

_Source: video, approximately 05:40. The slide shows the OperatorHub console and its Operator catalog._

### Operator Types Available through OperatorHub

The lesson identifies these categories:

| Operator type           | Description from the source                                                      |
| ----------------------- | -------------------------------------------------------------------------------- |
| **Red Hat operators**   | Operators provided as Red Hat Operators                                          |
| **Certified operators** | Operators from independent service vendors partnered with Red Hat                |
| **Community operators** | Operators from the open-source community but not officially supported by Red Hat |
| **Custom operators**    | Operators defined by users                                                       |

OperatorHub can also be used to install tools from the Kubernetes ecosystem.

The lesson gives **Istio Service Mesh** as an example.

### OperatorHub Visual Details

The video slide explicitly shows that OperatorHub:

* Installs Operators with a simple click.
* Has many Operators available.
* Organizes categories including Red Hat, Certified, Community, and Custom.
* Can be used to install other Kubernetes ecosystem tools.

## Operator Maturity Model

The lesson states that the sophistication of Operator management logic varies according to:

* The type of service represented by the Operator.

The **Operator Maturity Model** defines phases of maturity for general day-to-day operation activities.

The maturity scale ranges from:

```
Basic Install → Autopilot
```

The video provides five maturity levels.

### Level I — Basic Install

Focus:

* Automated application provisioning.
* Configuration management.

### Level II — Seamless Upgrades

Focus:

* Patch upgrades.
* Minor version upgrades.
* Changes that are often supported.

### Level III — Full Lifecycle

Focus:

* Application lifecycle.
* Storage lifecycle.
* Backup.
* Failure recovery.

### Level IV — Deep Insights

Focus:

* Metrics.
* Alerts.
* Log processing.
* Workload analysis.

### Level V — Auto Pilot

Focus:

* Horizontal scaling.
* Vertical scaling.
* Automatic configuration tuning.
* Anomaly detection.
* Scheduling tuning.

### Maturity Model Visual

_Source: video, approximately 04:20. The visual shows Levels I–V from Basic Install through Auto Pilot and maps the Helm, Ansible, and Go capabilities of the Operator SDK across the maturity progression._

> ⚠️ **Unclear in source:** The visual maturity slide contains capability-span bars for Helm, Ansible, and Go. The exact start/end boundaries of those spans are presented graphically but are not specified numerically in the narration, so this document does not assign unsupported exact level boundaries beyond what is visibly represented.

## Operator Examples

The lesson gives these Operator examples:

1. Deploying an application to an OpenShift cluster.
2. Scaling an application with the help of multiple replicas based on the application type.
3. Automating routine tasks in a cluster, such as:
   * Taking backups of application state.
   * Restoring application state from backups.
4. Integration.

_Source: video, approximately 04:50. The slide visually introduces examples including application deployment, scaling with multiple replicas, and backup/restore automation._

## Operators in Practice

The lesson gives a concrete pattern for deploying a complete application.

### Steps

1. Create a custom resource (CR) for the application.
2. Create a custom controller for the CRD.
3. Use Operator logic to determine how to reconcile the actual and desired/configured states.
4. The CRD requires creation of:
   * Deployments.
   * Services.
   * Storage.
   * Other objects.

### Practical Flow

```
Application
    ↓
Custom Resource
    ↓
Custom Controller
    ↓
Operator Logic
    ↓
Reconcile Actual vs Desired State
    ↓
Create / Manage:
  ├── Deployments
  ├── Services
  ├── Storage
  └── Other Objects
```

_Source: video, approximately 05:10. The slide shows the four-step application-deployment process and the resulting Deployments, Services, Storage, and other objects._

## Operator Deployment and Reconciliation Flow

The complete operator-driven application model can be represented as:

```
User / Developer
      │
      │ creates/changes
      ▼
Custom Resource
      │
      │ watched by
      ▼
Operator / Custom Controller
      │
      │ reads desired state
      ▼
Kubernetes API
      │
      │ creates / updates
      ▼
Cluster Resources
 ┌──────────┬──────────┬──────────┬──────────────┐
 │ Deployments │ Services │ Storage │ Other objects │
 └──────────┴──────────┴──────────┴──────────────┘
      │
      ▼
Actual Cluster State
      │
      └──────── reconcile ────────┐
                                  ▼
                           Desired State
```

The relationship is continuous rather than a one-time install process because the Operator continually watches and makes decisions based on the current state.

## Benefits and Capabilities Reference

The lesson's capabilities can be grouped as follows.

| Category               | Capabilities stated in the source                              |
| ---------------------- | -------------------------------------------------------------- |
| Installation           | Repeatable installs and upgrades                               |
| Health                 | Regular full-system health checks of each component            |
| Updates                | Over-the-air updates                                           |
| Knowledge              | Collect and spread knowledge from field engineers to all users |
| Integration            | APIs and CLI tools such as `kubectl` and `OC`                  |
| Application lifecycle  | Creation, configuration, deployment, management                |
| Cluster operations     | Upgrades, failover, scaling                                    |
| Automation             | Routine tasks such as backup and restore                       |
| Declarative management | CRDs + custom controllers                                      |
| Ecosystem              | Operator SDK, OLM, Registry, OperatorHub                       |
| Application resources  | Deployments, Services, Storage, and other objects              |

## Command Reference

The lesson references CLI tooling but does **not** provide complete executable command syntax, flags, arguments, namespaces, or command examples.

### CLI Tools Mentioned

| Command / tool reference | Purpose                                                        | Syntax / Example | Notes                                                                   |
| ------------------------ | -------------------------------------------------------------- | ---------------- | ----------------------------------------------------------------------- |
| `kubectl`                | Access CRD objects and interact through Kubernetes CLI tooling | `kubectl`        | The source names the CLI but does not provide a full command invocation |
| `OC`                     | CLI integration mentioned as part of Operator capabilities     | `OC`             | The source refers to “OC commands” but provides no executable syntax    |

```
kubectl
OC
```

> **Important:** These are CLI tool names referenced by the lesson, not complete commands demonstrated in the source. No unsupported command syntax has been added.

## Video Visual Context

The MP4 was inspected for slide-level information. The visuals primarily reinforce the narrated content and add diagrams, tables, and maturity-level labels.

### Visual Sequence

| Approx. video time | Visual                                                       |
| -----------------: | ------------------------------------------------------------ |
|            \~00:35 | Operator introduction and Kubernetes API interaction diagram |
|            \~01:35 | Why use Operators — feature boxes                            |
|            \~01:55 | Service Brokers vs Operators comparison                      |
|            \~02:35 | Custom Resource Definition (CRD)                             |
|            \~03:15 | Custom controllers and reconciliation                        |
|            \~03:35 | Operator Framework                                           |
|            \~04:20 | Operator Maturity Model                                      |
|            \~04:50 | Operator examples                                            |
|            \~05:10 | Operators in practice                                        |
|            \~05:40 | OperatorHub                                                  |
|            \~06:15 | Recap                                                        |

### Recap Slide

_Source: video, approximately 06:15. The recap slide visually summarizes CRDs, custom controllers, the Operator Pattern, automated cluster tasks, the Operator Framework, and the Operator Maturity Model._

## Key Terms / Glossary

| Term                        | Definition / meaning from the source                                                                              |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Operator**                | Software that automates cluster tasks and acts as a custom controller to extend the Kubernetes API                |
| **Custom Controller**       | Controller that reconciles custom resources and the cluster state                                                 |
| **CRD**                     | Custom Resource Definition; stores and retrieves objects in the Kubernetes API and extends the API                |
| **Custom Resource (CR)**    | A custom object used with a CRD as the desired state                                                              |
| **Operator Pattern**        | Combining CRDs and custom controllers to create a declarative API                                                 |
| **Declarative API**         | API created by pairing CRDs and custom controllers so desired state can be reconciled with actual state           |
| **Reconciliation**          | Aligning actual cluster state with desired/configured state                                                       |
| **Operator Framework**      | Open-source toolset covering coding, testing, delivery, and Operator updates                                      |
| **Operator SDK**            | Framework component that helps authors build, test, and package Operators                                         |
| **Helm**                    | Operator SDK capability named by the lesson                                                                       |
| **Go**                      | Operator SDK capability named by the lesson                                                                       |
| **Ansible**                 | Operator SDK capability named by the lesson                                                                       |
| **OLM**                     | Operator Lifecycle Manager; controls Operator install, upgrade, and RBAC                                          |
| **RBAC**                    | Role-Based Access Control; the source says OLM controls Operator RBAC                                             |
| **Operator Registry**       | Stores CRDs, CSVs, and Operator metadata for packages and channels                                                |
| **CSV**                     | Cluster Service Version                                                                                           |
| **OperatorHub**             | Web console for finding and installing Operators                                                                  |
| **Service Broker**          | Short-running process described in the lesson as unable to perform consecutive-day upgrades, failover, or scaling |
| **Human Operator**          | Person who understands the system, deployment, and problem-fixing process                                         |
| **Software Operator**       | Software representation of human Operator knowledge and processes                                                 |
| **Operator Maturity Model** | Model describing phases of Operator management maturity from Basic Install to Auto Pilot                          |
| **OTA**                     | Over-the-air                                                                                                      |
| **Off-cluster service**     | Service category explicitly mentioned in the Service Broker vs Operator comparison                                |
| **Istio Service Mesh**      | Example Kubernetes ecosystem tool that can be installed via OperatorHub                                           |

## Complete Lesson Walkthrough

### Introduction

The lesson introduces Operators as a way to automate cluster tasks and extend the Kubernetes API through custom controllers.

### Operator Execution Model

Operators:

* Run in pods.
* Interact with the API server.
* Make continuous real-time decisions.
* Package, deploy, and manage Kubernetes applications.

### Operational Knowledge

The human-versus-software Operator distinction explains the basic motivation:

```
Human knowledge
     ↓
Operator logic
     ↓
Automated operations
```

### Operational Capabilities

Operators provide:

* Repeatable installation/upgrades.
* Full-system health checks.
* OTA updates.
* Knowledge distribution.
* API/CLI integration.

### Service Broker Comparison

Service Brokers are described as short-running, while Operators are long-running and continuously observe cluster state.

### API Extension

CRDs extend Kubernetes beyond built-in resources.

### Reconciliation

Custom controllers reconcile desired and actual state.

### Operator Pattern

CRDs + custom controllers produce a declarative API known as the Operator Pattern.

### Framework

The Operator Framework provides:

* Operator SDK.
* Operator Lifecycle Manager.
* Operator Registry.

### Marketplace

OperatorHub allows cluster administrators to locate and install Operators.

### Maturity

Operator capabilities progress from:

```
Basic Install
→ Seamless Upgrades
→ Full Lifecycle
→ Deep Insights
→ Auto Pilot
```

### Practical Use

Operators can:

* Deploy applications.
* Scale applications.
* Automate backup/restore tasks.
* Provide integrations.

### Application Deployment Pattern

```
Custom Resource
      ↓
Custom Controller
      ↓
Reconciliation Logic
      ↓
Deployments + Services + Storage + Other Objects
```

## Source Notes

### Transcript Agreement

The TXT and VTT spoken content match exactly after whitespace normalization.

The VTT contains **116 timed cues**, while the TXT is supplied as a single continuous line. The difference is formatting/segmentation, not missing spoken content.

### Video Scope

The MP4 was inspected directly. Visual material primarily adds:

* Architecture diagrams.
* Comparison tables.
* Component relationships.
* Maturity-level labels.
* Practical process steps.
* OperatorHub interface imagery.
* Recap structure.

### Unclear / Ambiguous Items

> ⚠️ **Unclear in source:** The phrase describing Service Brokers and Operators includes “off-cluster services” on both sides of the comparison. Both occurrences are preserved.

> ⚠️ **Unclear in source:** The source uses “CRDs paired with custom controllers” as the Operator Pattern and describes the result as a “declarative API.” No further formal definition of declarative API is supplied.

> ⚠️ **Unclear in source:** The maturity-model slide visually maps Helm, Ansible, and Go to maturity ranges, but the narration does not state exact endpoint levels. The visual is preserved without inventing exact boundaries.

> ⚠️ **Unclear in source:** The source says custom builds? No — this lesson does not discuss Builds; that topic belongs to separate lesson material and is not included here.

### Source Terminology Preserved

The lesson's terminology is retained, including:

* “Operator”
* “Operator Pattern”
* “custom controller”
* “custom resource definition”
* “CRD”
* “Operator SDK”
* “Operate Framework”
* “Operator Lifecycle Manager”
* “Operator Registry”
* “Operator Hub”
* “Operator Maturity Model”
* “Auto Pilot”
* “OTA”
* “CSV”
* “RBAC”

### Completeness Check

* Every topic in the supplied TXT is represented.
* Every topic in the VTT is represented.
* Video-only visual information observed during inspection is incorporated.
* No executable command syntax was invented.
* Ambiguous source statements are explicitly flagged.
* The transcript is merged once rather than duplicated.

## Original Transcript Coverage

The complete spoken transcript is represented in the structured sections above, in source order, without dropping any substantive concept, example, or comparison. The VTT is not reproduced separately because its text matches the TXT exactly; its timestamp information is represented through the visual/timeline navigation rather than duplicating the same spoken content.

## Final Recall Chain

```
Operator
   ↓
Automates Cluster Tasks
   ↓
Custom Resource (CRD)
   +
Custom Controller
   ↓
Operator Pattern
   ↓
Declarative API
   ↓
Continuous Reconciliation
   ↓
Operator Framework
   ├── SDK
   ├── OLM
   └── Registry
   ↓
OperatorHub
   ↓
Maturity: Basic Install → Auto Pilot
```

# Kubernetes Objects Part 1

<figure><img src="../.gitbook/assets/Kubernetes Objects Mind Map Part 1.png" alt=""><figcaption></figcaption></figure>

## Learning Objectives

After watching this video, you will be able to:

1. Define a Kubernetes object and its properties.
2. Describe basic Kubernetes objects and their features.
3. Demonstrate how Kubernetes objects relate to each other.

## Object Fundamentals

In the real world, an object is something that has an identity, a state, and a behavior. A window or a shopping cart are examples of objects.

A software object is a bundle of data that has an identity, a state, and a behavior. Examples include variables, data structures, and specific functions.

An **entity** also has an identity and associated data. For example, in banking, a customer account is an entity.

**Persistent** means something will last even if there is a server failure or network attack. An example is persistent storage.

## Kubernetes Objects

Kubernetes objects are persistent entities. Examples include Pods, Namespaces, ReplicaSets, Deployments, and more.

Kubernetes objects consist of two main fields:

| Field       | Provided by | Purpose                                   |
| ----------- | ----------- | ----------------------------------------- |
| Object spec | User        | Dictates an object's desired state        |
| Status      | Kubernetes  | Describes the current state of the object |

Kubernetes works toward matching the current state to the desired state.

```
Object Spec
    ↓
Desired State

Status
    ↓
Current State

Kubernetes works toward:
Current State = Desired State
```

You can work with Kubernetes objects using:

* The Kubernetes API directly
* Client libraries
* The `kubectl` command-line interface
* A combination of these

## Labels

Labels are key-value pairs attached to objects. They are intended for identification of objects.

However, a label does not uniquely identify a single object. Many objects can have the same labels, which helps organize and group objects.

```
Label:
app = nginx

Pod A → app=nginx
Pod B → app=nginx
Pod C → app=nginx
```

### Label Selectors

Label selectors are the core grouping method in Kubernetes. They allow you to identify a set of objects.

```
Label Selector
       ↓
Matches labels
       ↓
Set of Kubernetes objects
```

## Namespaces

Namespaces provide a mechanism for isolating groups of resources within a single cluster.

They are useful when teams share a cluster for cost-saving purposes or for maintaining multiple projects in isolation. Namespaces are ideal when the number of cluster users is large.

| Namespace    | Intended use        |
| ------------ | ------------------- |
| `KubeSystem` | System users        |
| `default`    | Users' applications |

### Namespace Patterns

{% tabs %}
{% tab title="One team and one project" %}
There may be only one namespace for a user who works with one team, which only has one project deployed into a cluster.

```
User
  ↓
Team
  ↓
One Project
  ↓
One Namespace
```
{% endtab %}

{% tab title="Multiple teams, projects, or users" %}
There may be many teams or projects, or many users with different needs, where additional namespaces may be created.

```
Cluster
├── Namespace A → Team / Project A
├── Namespace B → Team / Project B
├── Namespace C → Team / Project C
└── ...
```
{% endtab %}
{% endtabs %}

Namespaces provide a scope for the names of objects. Each object must have a unique name for that resource type within that namespace.

## Pods

A Pod is the simplest unit in Kubernetes. A Pod represents a process or a single instance of an application running in the cluster.

A Pod usually wraps one or more containers. Creating replicas of a Pod serves to scale an application horizontally.

```
Pod
├── Container
└── Container
```

## YAML Object Definitions

YAML files are often used to define the object that you want to create.

The YAML file shown defines a simple Pod.

### Pod Fields

```yaml
kind: Pod
spec:
  containers:
    # container definition
    # name: nginx
    # image: image to run
    # ports: exposed container ports
```

<div align="left"><figure><img src="../.gitbook/assets/image (11).png" alt="" width="251"><figcaption></figcaption></figure></div>

| Field or concept | Meaning                                                      |
| ---------------- | ------------------------------------------------------------ |
| `kind`           | Specifies the kind of object to be created                   |
| `spec`           | Provides the appropriate fields for the object being created |
| `containers`     | Defines the containers that run in the Pod                   |
| Container name   | The example container is named `nginx`                       |
| `image`          | Dictates which image will run in the Pod                     |
| `ports`          | Lists the ports that the container exposes                   |

A Pod spec must contain at least one container.

> The transcript identifies these fields and concepts but does not provide the complete YAML file.

## ReplicaSets

A ReplicaSet is a set of identical running replicas of a Pod that are horizontally scaled.

```
ReplicaSet
├── Pod
├── Pod
├── Pod
└── ...
```

The configuration files for a ReplicaSet and a Pod are different from each other.

<div align="left"><figure><img src="../.gitbook/assets/image (12).png" alt="" width="309"><figcaption></figcaption></figure></div>

### `replicas`

The `replicas` field specifies the number of replicas that should be running at any given time.

Whenever this field is updated, the ReplicaSet creates or deletes Pods to meet the desired number of replicas.

```
Desired replicas
        ↓
ReplicaSet
        ↓
Creates or deletes Pods
        ↓
Maintains desired count
```

### Pod Template

A Pod template is included in the ReplicaSet spec. It defines the Pods that should be created by the ReplicaSet.

```
ReplicaSet
    ↓
Pod Template
    ↓
Creates Pods
```

### Selector and Match Labels

Under the `Selector` field, the labels supplied in the `Match Labels` field specify the Pods that can be acquired by the ReplicaSet.

The label identified in `Match Labels` is the same as the `Labels` field in the Pod template. Both are `app nginx`.

```
ReplicaSet Selector
        ↓
Match Labels
app: nginx
        ↓
Pod Template Labels
app: nginx
        ↓
Pods acquired by ReplicaSet
```

> Creating ReplicaSets directly is not recommended.

## Deployments

Instead, create a Deployment. A Deployment is a higher-level concept that manages ReplicaSets and offers more features and better control.

A Deployment is a higher-level object that provides updates for both Pods and ReplicaSets. Deployments run multiple replicas of an application using ReplicaSets and offer additional management capabilities.

| Application type | Kubernetes object |
| ---------------- | ----------------- |
| Stateless        | Deployment        |
| Stateful         | Stateful Set      |

Deployments can be used for:

* Deploying a replicated application
* Managing Pod updates
* Scaling up an application

### Deployment Specification

```yaml
kind: Deployment

spec:
  replicas:
  selector:
  template:
```

<div align="left"><figure><img src="../.gitbook/assets/image (13).png" alt="" width="323"><figcaption></figcaption></figure></div>

A Deployment specification identifies:

* The number of replicas
* A selector to identify which Pods can be acquired
* A Pod template

> The transcript does not provide the complete Deployment manifest.

## Rolling Updates

One key feature provided by Deployments, but not ReplicaSets, is rolling updates.

{% stepper %}
{% step %}
## Scale up the new version

A rolling update scales up a new version to the appropriate number of replicas.
{% endstep %}

{% step %}
## Scale down the old version

The rolling update scales down the old version to zero replicas.
{% endstep %}
{% endstepper %}

During a rolling update:

```
Deployment
    ↓
New version ReplicaSet
    ↓
Scale new version up
    ↓
Old version ReplicaSet
    ↓
Scale old version down to zero
```

The ReplicaSet ensures that the appropriate number of Pods exist, while the Deployment orchestrates the rollout of a new version.

## Object Relationships

```
Namespace
    ↓
Scopes object names and resources

Deployment
    ↓
Manages ReplicaSet
    ↓
Manages desired number of Pods
    ↓
Pods
    ↓
One or more Containers
```

```
Kubernetes Cluster
│
├── Namespace(s)
│    │
│    ├── Deployment
│    │    └── ReplicaSet
│    │         └── Pod(s)
│    │              └── Container(s)
│    │
│    └── Other Kubernetes Objects
│
└── Other Namespace(s)
```

## Desired State and Reconciliation

```
User
 ↓
Object Specification
 ↓
Desired State
 ↓
Kubernetes API / Client Library / kubectl
 ↓
Kubernetes
 ↓
Current Status
 ↓
Reconciliation
 ↓
Actual State approaches Desired State
```

This principle also appears in ReplicaSets:

```
Desired replica count
        ↓
ReplicaSet
        ↓
Actual Pod count
        ↓
Creates or deletes Pods
        ↓
Matches desired count
```

## Summary

* Kubernetes objects are persistent entities.
* Their main fields are object spec and status.
* The object spec describes desired state.
* Status describes current state.
* Kubernetes works toward matching current state to desired state.
* Labels are key-value pairs used to identify, organize, and group objects.
* Label selectors identify a set of objects.
* Namespaces isolate groups of resources within a single cluster and scope object names.
* Pods represent a process or an instance of an application running in the cluster.
* Pods usually wrap one or more containers.
* Pod replicas provide horizontal scaling.
* ReplicaSets create and manage horizontally scaled running Pods.
* ReplicaSets maintain a desired number of Pod replicas.
* Creating ReplicaSets directly is not recommended.
* Deployments manage ReplicaSets and provide updates for Pods and ReplicaSets.
* Deployments are suitable for stateless applications.
* Stateful Sets are used for stateful applications.
* Deployments provide rolling updates.

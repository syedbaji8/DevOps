# Kubernetes Objects Part 2

<figure><img src="../.gitbook/assets/Kubernetes Objects Mind Map Part 2.png" alt=""><figcaption></figcaption></figure>

## Learning Objectives

After watching this video, you will be able to:

1. Describe the purposes, properties, and uses of a **Service**.
2. Describe the roles and uses of:
   * ClusterIP
   * NodePort
   * LoadBalancer
   * ExternalName Services
3. Describe the roles and uses of:
   * Ingress
   * DaemonSet
   * StatefulSet
   * Job

## Kubernetes Service

A **Service** is a REST object, like Pods. It is a logical abstraction for a set of Pods in a cluster.

<div align="left"><figure><img src="../.gitbook/assets/image (14).png" alt="" width="375"><figcaption></figcaption></figure></div>

Services:

* Provide policies for accessing Pods in the cluster.
* Act as a load balancer across Pods.
* Receive a unique IP address for accessing applications deployed on Pods.
* Eliminate the need for a separate service-discovery process.
* Support TCP, UDP, and other protocols.
* Support multiple port definitions.
* Can use an optional selector.
* Can optionally map incoming ports to a target port.

The port number with the same name can vary in each backend Pod.

| Characteristic       | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| Object type          | REST object                                                  |
| Represents           | A logical abstraction for a set of Pods                      |
| Access               | Provides policies for accessing Pods                         |
| Traffic distribution | Acts as a load balancer across Pods                          |
| Addressing           | Each Service receives a unique IP address                    |
| Service discovery    | Eliminates the need for a separate service-discovery process |
| Protocols            | TCP, UDP, and others                                         |
| Port definitions     | Multiple port definitions                                    |
| Selector             | Optional                                                     |
| Target port mapping  | Optional                                                     |

## Service Discovery

Pods in a cluster can be destroyed, and new Pods can be created at any time. This volatility causes discoverability issues because Pod IP addresses can change.

A Service keeps track of Pod changes and exposes:

* A single IP address, or
* A DNS name.

Services use selectors to target a set of Pods.

```
Clients
  ↓
Stable Service IP / DNS name
  ↓
Service selector
  ↓
Current matching Pods
```

For native Kubernetes applications, API endpoints are updated whenever changes are detected to the Pods in the Service.

For non-native applications, Kubernetes uses a virtual-IP-based bridge or load balancer between the applications and the backend Pods.

## Service Types

Kubernetes provides four Service types:

| Service type | Main role                                                  |
| ------------ | ---------------------------------------------------------- |
| ClusterIP    | Internal cluster access; default and most common type      |
| NodePort     | Exposes a Service on each node at a static port            |
| LoadBalancer | Uses an external load balancer to expose and route traffic |
| ExternalName | Maps a Service to a DNS name using `spec.externalName`     |

{% tabs %}
{% tab title="ClusterIP" %}
**ClusterIP** is the default and most common Service type.<img src="../.gitbook/assets/image (15).png" alt="" data-size="original">

Kubernetes assigns a cluster-internal IP address to a ClusterIP Service, making it reachable only within the cluster. A ClusterIP Service cannot be used to make requests to the Service from outside the cluster.

You can set the ClusterIP address in the Service definition file.

ClusterIP provides inter-service communication within the cluster, such as communication between front-end and back-end components.

```
Front End
   |
   v
ClusterIP Service
   |
   v
Back End Pods
```
{% endtab %}

{% tab title="NodePort" %}
**NodePort** is an extension of ClusterIP Service.

<div align="left"><figure><img src="../.gitbook/assets/image (16).png" alt="" width="260"><figcaption></figcaption></figure></div>

A NodePort Service:

* Creates a NodePort.
* Routes incoming requests automatically to the ClusterIP Service.
* Exposes the Service on each node's IP address.
* Uses a static port.

```
Incoming Request
      ↓
Node IP : Static Port
      ↓
NodePort Service
      ↓
ClusterIP Service
      ↓
Backend Pods
```

{% hint style="warning" %}
For security purposes, production use is not recommended.
{% endhint %}

Kubernetes exposes a single Service with no load-balancing requirements for multiple Services.
{% endtab %}

{% tab title="LoadBalancer" %}
An external load balancer, or **ELB**, is an extension of the NodePort Service.![](<../.gitbook/assets/image (17).png>)

An ELB:

* Creates NodePort and ClusterIP Services automatically.
* Integrates with the NodePort Service.
* Automatically directs traffic to the NodePort Service.

```
Internet / External Traffic
            ↓
   External Load Balancer
            ↓
         NodePort
            ↓
        ClusterIP
            ↓
        Backend Pods
```

To expose a Service to the Internet, you need a new ELB with an IP address. You can use a cloud provider's ELB to host your cluster.
{% endtab %}

{% tab title="ExternalName" %}
The **ExternalName** Service type:

<div align="left"><figure><img src="../.gitbook/assets/image (18).png" alt="" width="223"><figcaption></figcaption></figure></div>

* Maps to a DNS name.
* Does not use a selector.
* Requires the `spec.externalName` parameter.

The ExternalName Service maps the Service to the contents of the external-name field, which returns a CNAME record and its value.

```yaml
spec:
  externalName: <external-dns-name>
```

You can use an ExternalName Service to:

* Create a Service that represents external storage.
* Enable Pods from different namespaces to talk to each other.
{% endtab %}
{% endtabs %}

## Ingress

{% columns %}
{% column %}
**Ingress** is an API object that, when combined with a controller, provides routing rules to manage external user access to multiple Services in a Kubernetes cluster.

In production, Ingress exposes applications to the Internet through:

|  Port | Protocol |
| ----: | -------- |
|  `80` | HTTP     |
| `443` | HTTPS    |
{% endcolumn %}

{% column %}
<figure><img src="../.gitbook/assets/image (21).png" alt="" width="234"><figcaption></figcaption></figure>
{% endcolumn %}
{% endcolumns %}



While the cluster monitors Ingress, an external load balancer is expensive and managed outside the cluster.

```
External Users
      ↓
   Ingress
      ↓
Routing Rules
   ├── Service A
   ├── Service B
   └── Service C
```

## DaemonSet

{% columns %}
{% column %}
A **DaemonSet** is an object that ensures nodes run a copy of a Pod.

{% stepper %}
{% step %}
## Add nodes

As nodes are added to a cluster, Pods are added to the nodes.
{% endstep %}

{% step %}
## Remove nodes

Pods are garbage collected when nodes are removed from a cluster.
{% endstep %}

{% step %}
## Delete the DaemonSet

If you delete a DaemonSet, all Pods managed by it are removed.
{% endstep %}
{% endstepper %}


{% endcolumn %}

{% column %}
<div align="left"><figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure></div>

DaemonSets are ideally used for:

* Storage.
* Logs.
* Monitoring nodes.
{% endcolumn %}
{% endcolumns %}

```
Cluster
├── Node 1 → DaemonSet Pod
├── Node 2 → DaemonSet Pod
├── Node 3 → DaemonSet Pod
└── New Node → DaemonSet Pod added
```

## StatefulSet

A **StatefulSet** is an object that:

* Manages stateful applications.
* Manages deployment and scaling of Pods.
* Provides guarantees about Pod ordering and uniqueness.
* Maintains a sticky identity for each Pod request.
* Provides persistent storage volumes for workloads.

```
Stateful Application
      ↓
StatefulSet
      ├── Pod deployment
      ├── Pod scaling
      ├── Ordering guarantees
      ├── Unique identities
      └── Persistent storage volumes
```

## Job

A **Job**:

<div align="left"><figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure></div>

* Creates Pods.
* Tracks the Pod completion process.
* Is retried until completed.
* Can run several Pods in parallel.

{% tabs %}
{% tab title="Delete a Job" %}
When a Job is deleted, the created Pods are removed.

```
Job deleted
   ↓
Created Pods removed
```
{% endtab %}

{% tab title="Suspend a Job" %}
When a Job is suspended, its active Pods are deleted until the Job resumes.

```
Job suspended
    ↓
Active Pods deleted
    ↓
Job resumes
    ↓
Job continues
```
{% endtab %}

{% tab title="CronJobs" %}
CronJobs are regularly used to create Jobs on an iterative schedule.

```
CronJob
   ↓
Scheduled time
   ↓
Create Job
   ↓
Create Pods
   ↓
Track completion
```
{% endtab %}
{% endtabs %}

## Object Comparison

| Object          | Main purpose                                                                                          |
| --------------- | ----------------------------------------------------------------------------------------------------- |
| **Service**     | Logical abstraction for a set of Pods; access policy; load balancing; stable IP/DNS                   |
| **Ingress**     | Routing rules for external user access to multiple Services when combined with a controller           |
| **DaemonSet**   | Ensures nodes run a copy of a Pod                                                                     |
| **StatefulSet** | Manages stateful applications, Pod deployment and scaling, identity, ordering, and persistent volumes |
| **Job**         | Creates Pods and tracks completion; retries until completed                                           |
| **CronJob**     | Regularly creates Jobs on an iterative schedule                                                       |

## Service Type Comparison

| Type             | Internal / External | Key behavior                                      | Source-specific note                                                 |
| ---------------- | ------------------- | ------------------------------------------------- | -------------------------------------------------------------------- |
| **ClusterIP**    | Internal            | Cluster-internal IP; default Service type         | Used for inter-service communication                                 |
| **NodePort**     | Node-accessible     | Static port on each node IP; routes to ClusterIP  | Production use is not recommended in the source for security reasons |
| **LoadBalancer** | External            | External load balancer routes traffic to NodePort | Creates NodePort and ClusterIP automatically                         |
| **ExternalName** | DNS-based           | Maps Service to DNS name/CNAME                    | Uses `spec.externalName`; no selector                                |

## Ingress vs. External Load Balancer

| Feature             | Ingress                                  | External Load Balancer               |
| ------------------- | ---------------------------------------- | ------------------------------------ |
| Type                | API object                               | External infrastructure/service      |
| Routing             | Provides routing rules with a controller | Directs traffic to NodePort          |
| Multiple Services   | Yes                                      | Not described as the primary role    |
| Internet access     | Port 80 / 443 in production              | Can expose a Service to the Internet |
| Management location | Cluster-monitored                        | Managed outside the cluster          |
| Cost statement      | Not described as expensive               | Described as expensive               |

## DaemonSet vs. StatefulSet vs. Job

| Characteristic       | DaemonSet                  | StatefulSet                     | Job                         |
| -------------------- | -------------------------- | ------------------------------- | --------------------------- |
| Main focus           | Node-level Pod presence    | Stateful application management | Completion of finite work   |
| Pod placement        | Across nodes               | Stateful application Pods       | As needed for Job execution |
| Identity             | Not source-highlighted     | Sticky identity                 | Not source-highlighted      |
| Ordering             | Not source-highlighted     | Ordering guarantees             | Not source-highlighted      |
| Persistent storage   | Storage use case mentioned | Persistent storage volumes      | Not source-highlighted      |
| Completion tracking  | No                         | No                              | Yes                         |
| Retry until complete | No                         | No                              | Yes                         |
| Parallel Pods        | Not source-highlighted     | Deployment/scaling              | Yes                         |

## Quick Reference

### Service

```
Logical abstraction over Pods
        ↓
Stable Service endpoint
        ↓
Selector targets Pods
        ↓
Load balancing / access policy
```

### Service Types

```
ClusterIP     → Internal cluster access
NodePort      → Node IP + static port
LoadBalancer  → External load balancer
ExternalName  → DNS / CNAME mapping
```

### Ingress

```
External users
      ↓
Ingress + Controller
      ↓
Routing rules
      ↓
Multiple Services
```

### DaemonSet

```
One Pod copy per node
```

### StatefulSet

```
Stateful app
+ Pod deployment/scaling
+ Ordering / uniqueness
+ Sticky identity
+ Persistent storage
```

### Job

```
Create Pods
   ↓
Track completion
   ↓
Retry until complete
```

### CronJob

```
Schedule
   ↓
Create Jobs repeatedly
```

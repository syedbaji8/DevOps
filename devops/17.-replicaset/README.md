# ReplicaSet

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

## Overview

This document captures the complete **ReplicaSet** lesson from the supplied TXT transcript, VTT subtitles, and the actual MP4 video. It explains why ReplicaSets are needed, how they maintain the desired number of Pods, how ReplicaSets relate to Deployments and Pod labels, how scaling works, and how Kubernetes automatically replaces missing Pods or removes extra Pods. The document also records commands and YAML that are visibly shown in the video, with the full transcript and complete VTT timing preserved at the end.

> **Source status:** TXT and VTT were both readable and their transcript content matches exactly after whitespace normalization. The MP4 video was also inspected directly, including the architecture/diagram slides and command demonstrations.

### Source verification

| Source                           | Result                                         |
| -------------------------------- | ---------------------------------------------- |
| `ReplicaSet(2).txt`              | 73 lines                                       |
| `ReplicaSet-subtitles-en(2).vtt` | 97 timed cues                                  |
| MP4 video                        | Readable and visually inspected                |
| TXT/VTT transcript comparison    | **Exact match after whitespace normalization** |
| Video-only details identified    | Yes                                            |
| Complete transcript preserved    | Yes                                            |
| Complete VTT timing preserved    | Yes                                            |

***

## Table of Contents

* [Learning Objectives](./#learning-objectives)
* [Single-Pod Deployment Limitations](./#single-pod-deployment-limitations)
* [ReplicaSet Introduction](./#replicaset-introduction)
* [ReplicaSet Desired-State Model](./#replicaset-desired-state-model)
* [ReplicaSet Benefits](./#replicaset-benefits)
* [ReplicaSet, Deployments, and Pods](./#replicaset-deployments-and-pods)
* [Pod Labels and ReplicaSet Selection](./#pod-labels-and-replicaset-selection)
* [ReplicaSet Created from a Deployment](./#replicaset-created-from-a-deployment)
* [Creating a ReplicaSet from Scratch](./#creating-a-replicaset-from-scratch)
* [Scaling a Deployment](./#scaling-a-deployment)
* [Maintaining Desired State After Pod Deletion](./#maintaining-desired-state-after-pod-deletion)
* [Maintaining Desired State After an Extra Pod Is Created](./#maintaining-desired-state-after-an-extra-pod-is-created)
* [Complete Command Reference](./#complete-command-reference)
* [Complete ReplicaSet YAML Shown in the Video](./#complete-replicaset-yaml-shown-in-the-video)
* [Video-Observed Visual Details](./#video-observed-visual-details)
* [Key Terms and Glossary](./#key-terms-and-glossary)
* [Complete Source Transcript](./#complete-source-transcript)
* [Complete VTT Timing Reference](./#complete-vtt-timing-reference)
* [Source Notes](./#source-notes)

***

## Learning Objectives

The lesson states that after watching the video, you will be able to:

1. Define a ReplicaSet.
2. Explain how a ReplicaSet works.
3. List the benefits of using a ReplicaSet.

***

## Single-Pod Deployment Limitations

The lesson begins by explaining the limitations of deploying an application on a single Pod.

If an application is deployed on a single Pod, the Pod may be unable to handle certain situations.

The lesson describes these limitations and operational requirements:

* Requests may increase.
* Application demand may grow.
* Outages may occur.
* A single-Pod deployment cannot accommodate growing application demands.
* A single-Pod deployment cannot handle load balancing across Pods.
* A single Pod can represent a single point of failure.
* Redundant Pods can help handle outages.
* Redundant Pods can minimize downtime and service interruptions.
* High availability can be provided through redundant Pods.
* Deployments can be automatically restarted if something goes wrong.

### Video-observed slide

At approximately **00:00:40**, the video displays the slide **“Single pod deployment limitations”** with this list:

* Accommodate growing demands
* Handle outages
* Minimize downtime

The slide reinforces the limitations described by the narration.

### Why redundancy matters

```
Single Pod
    |
    +--> Increased demand
    +--> Outage
    +--> Single point of failure
    +--> No redundancy
```

With multiple Pods:

```
                    Application
                        |
              +---------+---------+
              |         |         |
            Pod A     Pod B     Pod C
              |         |         |
              +---------+---------+
                        |
                   Redundancy
                        |
                 Higher availability
```

***

## ReplicaSet Introduction

The lesson introduces ReplicaSet as the way to work around the limitations of a single-Pod deployment.

A ReplicaSet:

* Ensures the right number of Pods are always up and running.
* Tries to match the actual state of replicas to the desired state.
* Adds Pods for scaling.
* Deletes Pods for scaling.
* Adds redundancy.
* Helps maintain availability.
* Replaces failing Pods.
* Deletes additional Pods when necessary.
* Maintains the desired state.
* Supersedes ReplicaController and should be used instead.

### Video-observed slide

At approximately **00:01:20**, the video displays **“ReplicaSet: Introduction”** and summarizes:

* A ReplicaSet adds or deletes Pods for scaling and redundancy.
* A ReplicaSet replaces failing Pods or deletes additional Pods to maintain the desired state.
* A ReplicaSet supersedes ReplicaControllers.

***

## ReplicaSet Desired-State Model

The central behavior of a ReplicaSet is maintaining the desired number of Pods.

The lesson states that a ReplicaSet:

> always tries to match the actual state of the replicas to the desired state.

### Desired state

The **desired state** is the number of replicas that should be running.

### Actual state

The **actual state** is the number of replicas that are currently running.

The ReplicaSet continually works to reconcile the two.

```
Desired State
     |
     v
ReplicaSet
     |
     v
Compare with Actual State
     |
     +----------------------+
     |                      |
 Actual < Desired       Actual > Desired
     |                      |
     v                      v
Create Pods             Delete Pods
     |                      |
     +----------+-----------+
                |
                v
        Desired State
        is maintained
```

***

## ReplicaSet Benefits

The lesson explains the main benefits of using a ReplicaSet.

### High availability

A ReplicaSet provides high availability through redundancy.

### Scaling

A ReplicaSet enables scaling by:

* Creating Pods.
* Deleting Pods.

### Failure recovery

When a managed Pod fails or is deleted, the ReplicaSet replaces it to restore the desired number.

### Excess-Pod correction

When an extra Pod causes the actual state to exceed the desired state, the ReplicaSet removes the extra Pod.

### Legacy controller replacement

The lesson states that ReplicaSet supersedes ReplicaController and should be used instead.

***

## ReplicaSet, Deployments, and Pods

A ReplicaSet is created when you create a Deployment in the cluster.

The lesson states that Deployments:

* Manage ReplicaSets.
* Send declarative updates to Pods.
* Provide many other useful features.

For this reason, the lesson says:

> A ReplicaSet is best managed by a Deployment.

### Recommended relationship

```
Deployment
    |
    v
ReplicaSet
    |
    v
Pods
```

### Best-practice statement from the lesson

The lesson explicitly says that creating a Deployment that includes a ReplicaSet is recommended over creating a standalone ReplicaSet.

***

## Pod Labels and ReplicaSet Selection

The lesson states that Kubernetes is designed to keep object types independent.

Because of this:

* The ReplicaSet does not own the Pods in the way the source describes ownership.
* Instead, the ReplicaSet uses Pod labels to decide which Pods to acquire when bringing the Deployment to the desired state.

### Deployment template

The lesson explains that the Deployment template's metadata defines:

* Labels.
* The spec of potential Pod candidates to add or delete.

### Relationship

```
Deployment Template
       |
       +--> metadata.labels
       |
       +--> Pod specification
       |
       v
Potential Pod candidates
       |
       v
ReplicaSet selector
       |
       v
Matching Pod labels
       |
       v
Pods acquired for desired state
```

### Video-observed slide

At approximately **00:01:40–00:01:50**, the video displays **“ReplicaSet | Deployments | Pods”** and states:

* Kubernetes keeps object types independent.
* A ReplicaSet does not own its Pods.
* It uses Pod labels.

This visual directly supports the narrated explanation.

***

## ReplicaSet Created from a Deployment

The lesson says a ReplicaSet is automatically created when a Deployment is created.

To verify this, the lesson instructs you to:

1. Create a Deployment.
2. Use a `get ReplicaSet` command.
3. Verify that the ReplicaSet was generated automatically.

The lesson also states that, in the demonstrated default scenario, the ReplicaSet replicates to one Pod.

If you describe the Pod, you can see:

* The Pod's details.
* That it is controlled by the same ReplicaSet.

### Video-observed verification

At approximately **00:02:00**, the video shows:

```bash
kubectl get deployment
```

with a Deployment named:

```
hello-kubernetes
```

The displayed Deployment has:

* `READY` = `1/1`
* `UP-TO-DATE` = `1`
* `AVAILABLE` = `1`

The video then shows the ReplicaSet relationship in the subsequent command output.

***

## Creating a ReplicaSet from Scratch

The lesson also explains how to create a ReplicaSet directly.

It says to:

* Apply a YAML file.
* Set the `kind` attribute to `ReplicaSet`.

If the number of replicas is set to `1`:

* One Pod is created.

The lesson compares this to creating a default configuration without explicitly specifying the number of replicas in the YAML.

> ⚠️ **Unclear in transcript-only source:** The transcript does not reproduce the full YAML shown on screen. The actual video does show the complete YAML, which is captured below.

### Video-observed YAML

At approximately **00:02:20**, the video displays:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: hello-kubernetes
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-kubernetes
  template:
    metadata:
      labels:
        app: hello-kubernetes
    spec:
      containers:
        - name: hello-kubernetes
          image: paulbouwer/hello-kubernetes:1.5
          ports:
            - containerPort: 8080
```

### What the visible YAML defines

| Field                           | Value shown in video              | Purpose in the shown configuration |
| ------------------------------- | --------------------------------- | ---------------------------------- |
| `apiVersion`                    | `apps/v1`                         | API version                        |
| `kind`                          | `ReplicaSet`                      | Defines the object type            |
| `metadata.name`                 | `hello-kubernetes`                | ReplicaSet name                    |
| `spec.replicas`                 | `1`                               | Desired replica count              |
| `spec.selector.matchLabels`     | `app: hello-kubernetes`           | Selects matching Pods              |
| `spec.template.metadata.labels` | `app: hello-kubernetes`           | Labels generated Pods              |
| Container `name`                | `hello-kubernetes`                | Container name                     |
| Container `image`               | `paulbouwer/hello-kubernetes:1.5` | Container image                    |
| `containerPort`                 | `8080`                            | Container port                     |

***

## Complete ReplicaSet YAML Shown in the Video

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: hello-kubernetes
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-kubernetes
  template:
    metadata:
      labels:
        app: hello-kubernetes
    spec:
      containers:
        - name: hello-kubernetes
          image: paulbouwer/hello-kubernetes:1.5
          ports:
            - containerPort: 8080
```

***

## Creating and Inspecting the Standalone ReplicaSet

The lesson says:

1. Use the create ReplicaSet command.
2. The output confirms the ReplicaSet was created.
3. Use the `get pods` command.
4. Observe the Pod status as `Running`.
5. Use the `get rs` command.
6. `rs` is short for ReplicaSet.
7. The output shows the name and other details of the ReplicaSet and its Pod.

### Create the ReplicaSet

The exact command is visible in the video at approximately **00:02:40**:

```bash
kubectl create -f replicaset.yaml
```

The video shows output confirming:

```
replicaset.apps/hello-kubernetes created
```

### Real command shown

```bash
kubectl create -f replicaset.yaml
```

### Get Pods

The video then shows:

```bash
kubectl get pods
```

The displayed Pod is:

```
hello-kubernetes-n4dsn
```

and its status is:

```
Running
```

### Get ReplicaSets

The video then shows:

```bash
kubectl get rs
```

The output identifies the ReplicaSet:

```
hello-kubernetes
```

with:

* `DESIRED = 1`
* `CURRENT = 1`
* `READY = 1`

### Video-observed command sequence

```bash
kubectl create -f replicaset.yaml
kubectl get pods
kubectl get rs
```

***

## Deployment Recommended Over Standalone ReplicaSet

The lesson repeats an important best-practice point:

> Creating a Deployment that includes a ReplicaSet is recommended over creating a standalone ReplicaSet.

The reason given in the lesson is that Deployments:

* Manage ReplicaSets.
* Send declarative updates to Pods.
* Provide many other useful features.

***

## Scaling a Deployment

Before scaling a Deployment, the lesson says you must ensure that you have:

* A Deployment.
* A Pod.

### Create the Deployment

The video shows the exact command at approximately **00:03:20**:

```bash
kubectl create -f deployment.yaml
```

The output is:

```
deployment.apps/hello-kubernetes created
```

The Deployment creates a Pod by default.

### Verify Pods

The lesson then uses:

```bash
kubectl get pods
```

The video shows the created Pod:

```
hello-kubernetes-5655b546f8-2nlqb
```

with:

```
READY   1/1
STATUS  Running
```

### Check the Deployment

The video shows:

```bash
kubectl get deploy
```

The Deployment is named:

```
hello-kubernetes
```

with the displayed status:

```
READY        1/1
UP-TO-DATE   1
AVAILABLE    1
```

***

## Scaling the Deployment to Three Replicas

Once the Deployment and Pod are in place, the lesson says to use the scale command to set the desired number of replicas.

The example sets:

```
replicas = 3
```

### Exact command shown in video

At approximately **00:04:00**:

```bash
kubectl scale deploy hello-kubernetes --replicas=3
```

The output shown is:

```
deployment.apps/hello-kubernetes scaled
```

### Verify the three Pods

The video immediately shows:

```bash
kubectl get pods
```

The output contains three Pods, including:

```
hello-kubernetes-5655b546f8-2nlqb
hello-kubernetes-5655b546f8-5mflw
hello-kubernetes-5655b546f8-hbt7v
```

All three are shown as:

```
READY    1/1
STATUS   Running
```

The lesson explains that the ReplicaSet created two new Pods:

* One ending in `5mflw`.
* One ending in `hbt7v`.

### Scaling flow

```
Deployment
    |
    v
ReplicaSet
    |
    +--> Existing Pod
    |
    +--> New Pod
    |
    +--> New Pod
    |
    v
3 running Pods
```

***

## Maintaining Desired State After Pod Deletion

The lesson next demonstrates how the ReplicaSet maintains desired state when a Pod is deleted.

At this point, the desired number of Pods is:

```
3
```

The three Pods are visible in the `get pods` output.

### Delete one Pod

The lesson deletes the Pod ending in:

```
5mflw
```

The video shows the exact command at approximately **00:04:30**:

```bash
kubectl delete pod hello-kubernetes-5655b546f8-5mflw
```

The output shown is:

```
pod "hello-kubernetes-5655b546f8-5mflw" deleted
```

### State mismatch

Immediately after deleting the Pod:

```
Desired state = 3
Actual state  = 2
```

The lesson explains that this mismatch causes the ReplicaSet to create a replacement automatically.

### Replacement Pod

The video shows a new Pod ending in:

```
6lw4r
```

The source narration states:

> The ReplicaSet immediately created a new Pod ending in 6lw4r.

The total number of Pods returns to:

```
3
```

### Video-observed visual

The video explicitly shows a highlighted message:

```
The desired state is maintained.
```

### Recovery flow

```
3 desired Pods
     |
     v
Delete Pod ...-5mflw
     |
     v
2 actual Pods
     |
     v
ReplicaSet detects mismatch
     |
     v
Creates replacement ...-6lw4r
     |
     v
3 actual Pods
     |
     v
Desired state maintained
```

***

## Maintaining Desired State After an Extra Pod Is Created

The lesson then demonstrates the opposite mismatch.

This time:

* Desired state remains `3`.
* An extra Pod is created.
* Actual state becomes `4`.

### Initial state

```
Desired = 3
Actual  = 3
```

The lesson starts by showing the existing three Pods.

### Create an extra Pod

The video shows the exact command at approximately **00:05:05**:

```bash
kubectl create pod hello-kubernetes-5655b546f8-mx9rp
```

The output shown is:

```
pod "hello-kubernetes-5655b546f8-mx9rp" created
```

### Verify the four Pods

The video shows:

```bash
kubectl get pods
```

At this point the output contains four Pods.

The extra Pod ends in:

```
mx9rp
```

### State mismatch

Now:

```
Desired state = 3
Actual state  = 4
```

The ReplicaSet strives to bring actual state back to desired state.

The lesson says the new Pod ending in `mx9rp` is:

* Marked for deletion.
* Removed automatically.

### Final state

After the extra Pod is removed:

```
Desired state = 3
Actual state  = 3
```

The lesson states that `get pods` again shows the total number of Pods restored to three.

### Video-observed visual

The video again highlights:

```
The desired state is maintained.
```

***

## Desired-State Reconciliation — Both Cases

The lesson demonstrates both directions of reconciliation.

### Case A — Too few Pods

```
Desired = 3
Actual  = 2

ReplicaSet
    ↓
Create Pod
    ↓
Desired = 3
Actual  = 3
```

### Case B — Too many Pods

```
Desired = 3
Actual  = 4

ReplicaSet
    ↓
Delete extra Pod
    ↓
Desired = 3
Actual  = 3
```

This is the central behavior demonstrated by the video.

***

## Video-Observed Visual Details

The MP4 adds several concrete visual details that are not completely recoverable from the TXT transcript alone.

### Visual 1 — Single-Pod limitation slide

Approximate time:

```
00:00:40
```

Visible heading:

```
Single pod deployment limitations
```

Visible bullets:

```
Accommodate growing demands
Handle outages
Minimize downtime
```

### Visual 2 — ReplicaSet introduction slide

Approximate time:

```
00:01:20
```

Visible heading:

```
ReplicaSet: Introduction
```

Visible points:

```
A ReplicaSet:
- Adds or deletes pods for scaling and redundancy
- Replaces failing pods or deletes additional pods to maintain the desired state
- Supersedes ReplicaControllers
```

### Visual 3 — Deployment / ReplicaSet / Pod relationship

Approximate time:

```
00:01:40–00:01:50
```

Visible heading:

```
ReplicaSet | Deployments | Pods
```

Visible concepts:

```
Kubernetes keeps object types independent.

A ReplicaSet does not own its Pods.
It uses pod labels.
```

### Visual 4 — ReplicaSet YAML

Approximate time:

```
00:02:20
```

The complete visible YAML is reproduced in the [Complete ReplicaSet YAML Shown in the Video](./#complete-replicaset-yaml-shown-in-the-video) section.

### Visual 5 — Create ReplicaSet

Approximate time:

```
00:02:40
```

Visible command:

```bash
kubectl create -f replicaset.yaml
```

Visible success output:

```
replicaset.apps/hello-kubernetes created
```

### Visual 6 — ReplicaSet inspection

Approximate time:

```
00:03:00
```

Visible commands:

```bash
kubectl get pods
kubectl get rs
```

### Visual 7 — Create Deployment

Approximate time:

```
00:03:20
```

Visible command:

```bash
kubectl create -f deployment.yaml
```

### Visual 8 — Scale Deployment

Approximate time:

```
00:04:00
```

Visible command:

```bash
kubectl scale deploy hello-kubernetes --replicas=3
```

Visible result:

```
deployment.apps/hello-kubernetes scaled
```

### Visual 9 — Delete Pod and self-heal

Approximate time:

```
00:04:30
```

Visible command:

```bash
kubectl delete pod hello-kubernetes-5655b546f8-5mflw
```

Visible replacement Pod:

```
hello-kubernetes-5655b546f8-6lw4r
```

### Visual 10 — Create extra Pod

Approximate time:

```
00:05:05
```

Visible command:

```bash
kubectl create pod hello-kubernetes-5655b546f8-mx9rp
```

The video shows the resulting four-Pod state and then the automatic removal of the extra Pod.

***

## Complete Command Reference

### ReplicaSet Creation and Inspection

| Command                                                | Purpose                                                 | Syntax / Example                                       | Notes                                          |
| ------------------------------------------------------ | ------------------------------------------------------- | ------------------------------------------------------ | ---------------------------------------------- |
| `kubectl create -f replicaset.yaml`                    | Create the ReplicaSet shown in the YAML                 | `kubectl create -f replicaset.yaml`                    | Exact command visible in video                 |
| `kubectl get pods`                                     | Inspect Pods                                            | `kubectl get pods`                                     | Used multiple times                            |
| `kubectl get rs`                                       | Inspect ReplicaSets                                     | `kubectl get rs`                                       | `rs` means ReplicaSet                          |
| `kubectl get deployment`                               | Inspect a Deployment                                    | `kubectl get deployment`                               | Video also visually uses the Deployment object |
| `kubectl get deploy`                                   | Inspect Deployments                                     | `kubectl get deploy`                                   | Exact abbreviated command visible in the video |
| `kubectl create -f deployment.yaml`                    | Create the Deployment used in the scale demo            | `kubectl create -f deployment.yaml`                    | Exact command visible in video                 |
| `kubectl scale deploy hello-kubernetes --replicas=3`   | Scale Deployment to three replicas                      | `kubectl scale deploy hello-kubernetes --replicas=3`   | Exact command visible in video                 |
| `kubectl delete pod hello-kubernetes-5655b546f8-5mflw` | Delete one Pod to demonstrate recovery                  | `kubectl delete pod hello-kubernetes-5655b546f8-5mflw` | Exact command visible in video                 |
| `kubectl create pod hello-kubernetes-5655b546f8-mx9rp` | Create an extra Pod for the desired-state demonstration | `kubectl create pod hello-kubernetes-5655b546f8-mx9rp` | Exact command visible in video                 |

### Command Sequence — Standalone ReplicaSet

```bash
kubectl create -f replicaset.yaml
kubectl get pods
kubectl get rs
```

### Command Sequence — Deployment and Scaling

```bash
kubectl create -f deployment.yaml
kubectl get pods
kubectl get deploy
kubectl scale deploy hello-kubernetes --replicas=3
kubectl get pods
```

### Command Sequence — Delete a Pod and Recover

```bash
kubectl get pods
kubectl delete pod hello-kubernetes-5655b546f8-5mflw
kubectl get pods
```

### Command Sequence — Create an Extra Pod and Recover

```bash
kubectl get pods
kubectl create pod hello-kubernetes-5655b546f8-mx9rp
kubectl get pods
```

***

## Complete ReplicaSet YAML Shown in the Video

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: hello-kubernetes
spec:
  replicas: 1
  selector:
    matchLabels:
      app: hello-kubernetes
  template:
    metadata:
      labels:
        app: hello-kubernetes
    spec:
      containers:
        - name: hello-kubernetes
          image: paulbouwer/hello-kubernetes:1.5
          ports:
            - containerPort: 8080
```

> This YAML is transcribed from the actual video frame. The transcript file itself does not contain all of these YAML lines.

***

## Key Terms and Glossary

| Term                        | Meaning in the lesson                                                                                                |
| --------------------------- | -------------------------------------------------------------------------------------------------------------------- |
| **ReplicaSet**              | Kubernetes object that ensures the right number of Pods are running and works to match actual state to desired state |
| **ReplicaController**       | Older controller that the lesson says is superseded by ReplicaSet                                                    |
| **Pod**                     | Application execution unit being replicated and managed                                                              |
| **Deployment**              | Higher-level object that manages ReplicaSets and sends declarative updates to Pods                                   |
| **Desired state**           | The target number/state of replicas                                                                                  |
| **Actual state**            | The current observed number/state of replicas                                                                        |
| **Redundancy**              | Using multiple Pods to reduce single points of failure                                                               |
| **High availability**       | Availability supported by redundant Pods                                                                             |
| **Scaling**                 | Increasing or decreasing the number of Pods                                                                          |
| **Pod label**               | Metadata used by the ReplicaSet to select matching Pods                                                              |
| **Deployment template**     | Template defining labels and specification for potential Pods                                                        |
| **Selector**                | Matching configuration used to identify the Pods associated with the ReplicaSet                                      |
| **`matchLabels`**           | Label matching configuration visible in the ReplicaSet YAML                                                          |
| **`replicas`**              | Desired number of Pods                                                                                               |
| **`rs`**                    | Short form for ReplicaSet in `kubectl get rs`                                                                        |
| **YAML descriptor**         | YAML configuration used to define Kubernetes resources                                                               |
| **Declarative update**      | Update approach described by the lesson as being managed through Deployment                                          |
| **Single point of failure** | A single Pod whose failure can affect availability                                                                   |

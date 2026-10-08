# Using kubectl

<figure><img src="../.gitbook/assets/Using kubectl_ Kubernetes Command Mind Map.png" alt=""><figcaption></figcaption></figure>

## Learning Objectives

After watching this lesson, you will be able to:

* Define `kubectl` and its command structure.
* List the three command types.
* Describe the features and advantages of the three command types.
* List commonly used commands with specific examples.

## What Is kubectl?

`kubectl` is the Kubernetes command-line interface, or CLI.

The transcript states that `kubectl` stands for “kube command tool line.”

`kubectl` is one of the key tools for working with Kubernetes. It helps users:

* Deploy applications.
* Inspect and manage cluster resources.
* View logs.
* Perform other Kubernetes cluster operations.

It is useful for users who work with Kubernetes clusters and manage running cluster workloads.

## The Three kubectl Command Types

1. Imperative commands
2. Imperative object configuration
3. Declarative object configuration

| Command type                     | Main idea                                                                            |
| -------------------------------- | ------------------------------------------------------------------------------------ |
| Imperative commands              | Directly create, update, and delete live objects                                     |
| Imperative object configuration  | Use a configuration file containing a full object definition and specify operations  |
| Declarative object configuration | Store desired state in configuration; Kubernetes determines the necessary operations |

## kubectl Command Structure

Keep each component in order:

```
kubectl command type name flags
```

| Component | Meaning                      | Examples/details from source       |
| --------- | ---------------------------- | ---------------------------------- |
| Command   | Operation to perform         | `create`, `get`, `apply`, `delete` |
| Type      | Resource type                | Pod, Deployment, ReplicaSet        |
| Name      | Resource name                | Used when applicable               |
| Flags     | Special options or modifiers | Override default values            |

## Imperative Commands

Imperative commands allow you to create, update, and delete live objects directly.

Specify the operation through arguments or flags.

They are easy to learn and easy to run.

To create a Pod with a specific container, specify a Pod name and the container image:

```
kubectl <create-operation> <pod-name> <container-image>
```

{% hint style="info" %}
This is a structural representation only. The complete executable command is not present in the source transcript.
{% endhint %}

### Advantages

* Easy to learn.
* Easy to run.
* Directly create, update, and delete live objects.
* Ideal for development and test environments.

### Limitations

| Limitation                   | Source explanation                            |
| ---------------------------- | --------------------------------------------- |
| No audit trail               | Important changes are harder to track         |
| Limited flexibility          | Options are limited                           |
| No templates                 | Commands do not provide reusable templates    |
| No change-review integration | Cannot integrate with change review processes |

### Shared-Deployment Problem

{% stepper %}
{% step %}
### Deploy an application

A developer runs a command to deploy an application.
{% endstep %}

{% step %}
### Another developer needs the same deployment

A second developer wants to deploy the same application, but there is no configuration file.
{% endstep %}

{% step %}
### Share the exact command

The second developer must contact the first developer, who must provide the exact command.
{% endstep %}

{% step %}
### Run the command

The second developer runs that command.
{% endstep %}
{% endstepper %}

A reusable template addresses this limitation.

```
Developer 1
   ↓
Imperative command
   ↓
Application deployed

No configuration file
   ↓
Developer 2 needs exact command
   ↓
Manual sharing of deployment steps
```

## Imperative Object Configuration

Imperative object configuration is a template-based approach.

The `kubectl` command specifies:

* Required operations.
* Optional flags.
* At least one file name.

The configuration file must contain a full object definition in YAML or JSON format.

### Example

```bash
kubectl create -f nginx.yaml
```

| Part         | Meaning            |
| ------------ | ------------------ |
| `kubectl`    | Kubernetes CLI     |
| `create`     | Create operation   |
| `-f`         | Specifies the file |
| `nginx.yaml` | Configuration file |

Using the same configuration templates in multiple environments produces identical results.

### Source Control and Change Processes

A configuration file may be stored in a source-control system such as:

```
Git
```

This approach:

* Can integrate with change processes.
* Provides audit trails.
* Provides templates for creating new objects.

### Advantages

| Benefit           | Source description                               |
| ----------------- | ------------------------------------------------ |
| Reusability       | Templates can be reused across environments      |
| Consistency       | Same configuration can produce identical results |
| Source control    | Files can be stored in Git                       |
| Change management | Can integrate with change processes              |
| Audit trail       | Provides audit history                           |
| Templates         | Provides reusable object definitions             |

### Requirements and Limitations

Using imperative object configuration requires:

* Understanding the object schema.
* Writing a YAML or JSON file.
* Specifying all necessary command operations.

#### Update Inconsistency Scenario

{% stepper %}
{% step %}
### Perform an update

A developer performs an update operation.
{% endstep %}

{% step %}
### Do not merge the update

The update is not merged into the configuration file.
{% endstep %}

{% step %}
### Use stale configuration

Another developer later uses the configuration.
{% endstep %}

{% step %}
### Deploy the previous configuration

The newer update is not represented, so the original or previous configuration is used.
{% endstep %}
{% endstepper %}

```
Developer performs update
          ↓
Update not merged into config file
          ↓
Shared configuration is stale
          ↓
Another developer deploys
          ↓
Previous/original configuration is used
```

## Declarative Object Configuration

Declarative object configuration defines the desired state in a shared configuration file rather than requiring users to specify every operation during deployment.

Kubernetes automatically determines the necessary operations.

Declarative object configuration:

* Stores configuration data in files.
* Identifies operations through `kubectl` rather than requiring the user to specify each operation.
* Works on directories and individual files.
* Is the ideal method for production systems.

### Declarative `apply` Command

The source describes `kubectl apply` being used with a directory to apply configuration data to all files in that directory.

```bash
kubectl apply
```

Conceptually:

```
kubectl apply <directory>
```

{% hint style="info" %}
The exact directory path is not supplied in the source transcript.
{% endhint %}

### Automation

With declarative object configuration:

* The user does not perform each individual operation.
* The system performs operations automatically.
* Configuration files define the desired state.
* Kubernetes actualizes that state.

```
Shared Configuration
        ↓
Desired State
        ↓
kubectl apply
        ↓
Kubernetes determines operations
        ↓
Kubernetes performs operations
        ↓
Current State
        ↓
Matches Desired State
```

### Single Source of Truth

When updates are made to a running application, the shared configuration template remains the source of truth.

Even if another developer misses several updates, they can apply the current configuration template to ensure the deployed object matches the expected configuration.

Kubernetes automatically:

* Determines the necessary operations.
* Performs the necessary operations.
* Matches the current state to the desired state.

## Comparison of Command Types

| Aspect                     | Imperative Commands            | Imperative Object Configuration               | Declarative Object Configuration           |
| -------------------------- | ------------------------------ | --------------------------------------------- | ------------------------------------------ |
| How operations are defined | User gives operations directly | User gives operations plus configuration file | User defines desired state                 |
| Configuration file         | Not required                   | Required                                      | Required                                   |
| YAML/JSON                  | Not required                   | Required                                      | Used for stored configuration              |
| Templates                  | No                             | Yes                                           | Yes                                        |
| Audit trail                | No                             | Yes                                           | Shared configuration provides traceability |
| Change review              | Not supported                  | Can integrate                                 | Configuration-based workflow               |
| User specifies operations  | Yes                            | Yes                                           | No; system determines operations           |
| Reusability                | Limited                        | High                                          | High                                       |
| Production suitability     | Ideal for development/test     | Has limitations                               | Ideal for production                       |

## Common kubectl Commands

| Command             | Purpose described in lesson                       | Concrete syntax provided?                             |
| ------------------- | ------------------------------------------------- | ----------------------------------------------------- |
| `kubectl create`    | Create objects defined in a file                  | Yes: `kubectl create -f nginx.yaml`                   |
| `kubectl get`       | Access or inspect resources                       | Command name only; complete variants not given        |
| `kubectl delete`    | Delete a file or container                        | Command name only                                     |
| `kubectl autoscale` | Apply auto-scaling process                        | Command name only                                     |
| `kubectl apply`     | Create or apply resources from YAML or JSON files | Command name; exact directory example not fully given |
| `kubectl scale`     | Scale the number of replicas                      | Command name; full example syntax not given           |

### `kubectl get`

The lesson states that `get` accesses a file, container, or any other resource.

```bash
kubectl get
kubectl get services
kubectl get pods -all-namespaces
kubectl get deployment my-dep
kubectl get pods
```

The examples mentioned include:

* Services in the current namespace.
* Pods in all namespaces.
* A particular Deployment.
* Pods in the current namespace.

### `kubectl delete`

The lesson states that `delete` deletes a file or container.

```bash
kubectl delete
```

### `kubectl autoscale`

The lesson states that `autoscale` applies the auto-scaling process to the selected file or container.

```bash
kubectl autoscale
```

### `kubectl apply`

The lesson states that `apply` creates resources using YAML or JSON files.

```bash
kubectl apply
kubectl apply -f ./my1.yaml -f ./my2.yaml
kubectl apply -f https://git.io/vPieo
```

Supported file extensions:

```
.yaml
.yml
.json
```

The command can create resources:

* From multiple files.
* From a URL.

### `kubectl scale`

The lesson states that `scale` changes the number of replicas.

```bash
kubectl scale
kubectl scale --replicas=3 rs/foo
kubectl scale --replicas=3 -f foo.yaml
```

Examples named in the source:

```
ReplicaSet name: foo
Replica count: 3

Resource file: resourceinfo.yaml
Replica count: 3
```

## Creating a Deployment with Three NGINX Replicas

The lesson gives this sequence:

{% stepper %}
{% step %}
### Create a Deployment

Create a Deployment configured with three replicas of the NGINX image.
{% endstep %}

{% step %}
### Use `apply`

Create the Deployment using the `apply` command.

`kubectl apply -f nginx.yaml`
{% endstep %}

{% step %}
### Confirm creation

Observe output confirming Deployment creation.

<mark style="color:$info;">deployment.apps/nginx-deployment created</mark>
{% endstep %}

{% step %}
### Inspect the Deployment

Use `get deployment` to inspect the Deployment.

`kubectl get deployment my-dep`
{% endstep %}

{% step %}
### Verify replicas

Confirm that three replicas are ready, up to date, and available.
{% endstep %}
{% endstepper %}

```
Deployment configuration
        ↓
3 replicas
        ↓
NGINX image
        ↓
kubectl apply
        ↓
Deployment created
        ↓
kubectl get deployment
        ↓
3 replicas:
- Ready
- Up to date
- Available
```

The source-backed command is:

```bash
kubectl apply
```

The source identifies the Deployment name as:

```
my-dep
```

The verification concept is:

```bash
kubectl get deployment
```

| Verification item   | Expected result stated in lesson |
| ------------------- | -------------------------------- |
| Deployment          | Created                          |
| Deployment name     | `my-dep`                         |
| Replicas ready      | 3                                |
| Replicas up to date | 3                                |
| Replicas available  | 3                                |

## Practical kubectl Workflow

```
Configuration file
       ↓
kubectl apply
       ↓
Deployment created
       ↓
kubectl get deployment
       ↓
Inspect:
  - Ready
  - Up to date
  - Available
```

## Imperative vs. Declarative Workflow

{% tabs %}
{% tab title="Imperative" %}
```
User
 ↓
Specify operation
 ↓
Specify resource
 ↓
Kubernetes executes operation
```
{% endtab %}

{% tab title="Imperative Object Configuration" %}
```
User
 ↓
Specify operation
 ↓
Configuration file
 ↓
Kubernetes creates/changes resources
```
{% endtab %}

{% tab title="Declarative" %}
```
User
 ↓
Shared configuration
 ↓
Desired state
 ↓
kubectl apply
 ↓
Kubernetes determines operations
 ↓
Kubernetes actualizes desired state
```
{% endtab %}
{% endtabs %}

## Development, Test, and Production

| Environment | Approach described by source              |
| ----------- | ----------------------------------------- |
| Development | Imperative commands can be ideal          |
| Test        | Imperative commands can be ideal          |
| Production  | Declarative object configuration is ideal |

## Quick Reference

### kubectl

```
Kubernetes CLI
```

### Command Structure

```
kubectl command type name flags
```

### Command Types

```
1. Imperative commands
2. Imperative object configuration
3. Declarative object configuration
```

### Most Important Source Example

```bash
kubectl create -f nginx.yaml
```

### Configuration Formats

```
YAML
YML
JSON
```

### Declarative Workflow

```
Configuration
    ↓
Desired State
    ↓
kubectl apply
    ↓
Kubernetes determines operations
    ↓
Actual State
```

### Production Approach

```
Declarative object configuration
```

## Lesson Conclusion

* `kubectl` is the Kubernetes command-line interface.
*   The command structure is:

    ```
    kubectl command type name flags
    ```
* Imperative commands are easiest to learn, have no audit trail, and are not flexible.
* Imperative object configuration uses templates to support deployment and replication workflows.
* Declarative object configuration is automated, requires no user input for individual operations, and is ideal for production systems.

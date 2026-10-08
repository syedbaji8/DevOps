# Lab-3 Introduction Kubernetes

## Lab Overview

This lab provides hands-on practice with:

* The Kubernetes `kubectl` CLI.
* Kubernetes Pods.
* Kubernetes Deployments.
* ReplicaSets.
* Kubernetes load balancing.

## Objectives

By completing the lab, you practice how to:

| Objective              | Description                                                            |
| ---------------------- | ---------------------------------------------------------------------- |
| Use `kubectl`          | Interact with a Kubernetes cluster from the command line               |
| Create a Pod           | Run a container image as a Pod                                         |
| Create a Deployment    | Manage multiple replicas through a Deployment                          |
| Create a ReplicaSet    | Maintain a target number of Pod replicas                               |
| Observe load balancing | Send repeated requests and observe traffic reaching different replicas |

## Cloud IDE and Environment

The lab is performed in a cloud development environment.

Before proceeding, verify that the command-line tools are available and that `kubectl` is configured to communicate with the lab cluster.

### Verify `kubectl`

```bash
kubectl version
```

The exact client and server versions can differ between environments.

Example environment:

```
Client Version:
v1.27.6

Kustomize Version:
v5.0.1

Server Version:
v1.26.13+IKS
```

{% hint style="info" %}
These version numbers are example environment values; they are not requirements for a current cluster.
{% endhint %}

### Retrieve the CC201 Repository

When it is not already present, clone the course repository:

```bash
[ ! -d 'CC201' ] && git clone \
  https://github.com/ibm-developer-skills-network/CC201.git
```

Inspect the working directory:

```bash
ls
```

Example files:

```
Dockerfile
app.js
hello-world-apply.yaml
hello-world-create.yaml
package.json
```

## Using the `kubectl` CLI

Kubernetes namespaces provide logical isolation within a cluster.

The lab environment already provides access to a Kubernetes namespace and configures `kubectl` to target the appropriate cluster and namespace.

### List Available Clusters

```bash
kubectl config get-clusters
```

The command displays the clusters known to the current kubeconfig.

Example format:

```
NAME
labs-prod-kubernetes-sandbox/c8ana0
```

### View Kubernetes Contexts

A `kubectl` context groups access parameters including:

* Cluster.
* User.
* Namespace.

```bash
kubectl config get-contexts
```

Example structure:

```
CURRENT   NAME        CLUSTER                              AUTHINFO   NAMESPACE
*         x-context   labs-prod-kubernetes-sandbox/c8ana0  x          sn-labs-x
```

### List Pods in the Current Namespace

```bash
kubectl get pods
```

The initial namespace may contain no user-created Pods:

```
No resources found in sn-labs-x namespace.
```

## Create a Pod with an Imperative Command

This section demonstrates direct imperative creation.

The application image is the `hello-world` image built and pushed to IBM Cloud Container Registry in the preceding lab.

{% stepper %}
{% step %}
## Set the Namespace as an Environment Variable

```bash
export MY_NAMESPACE=sn-labs-$USERNAME
```

The environment variable is reused in later commands.
{% endstep %}

{% step %}
## Build and Push the Container Image

```bash
docker build -t us.icr.io/$MY_NAMESPACE/hello-world:1 . && \
docker push us.icr.io/$MY_NAMESPACE/hello-world:1
```

This performs two operations:

1. Build the image and tag it with the target IBM Cloud Container Registry path.
2. Push the image to that registry.

### Image naming pattern

```
us.icr.io/<namespace>/hello-world:1
```
{% endstep %}

{% step %}
## Run the Image as a Kubernetes Pod

```bash
kubectl run hello-world \
  --image us.icr.io/$MY_NAMESPACE/hello-world:1 \
  --overrides='{"spec":{"template":{"spec":{"imagePullSecrets":[{"name":"icr"}]}}}}'
```

The `--overrides` option supplies an `imagePullSecrets` configuration so Kubernetes can pull the private image using the `icr` secret.

Expected result:

```
pod/hello-world created
```
{% endstep %}

{% step %}
## List the Pod

```bash
kubectl get pods
```

| Field      | Meaning                             |
| ---------- | ----------------------------------- |
| `NAME`     | Pod name                            |
| `READY`    | Ready containers / total containers |
| `STATUS`   | Current Pod state                   |
| `RESTARTS` | Container restart count             |
| `AGE`      | Pod age                             |

Example:

```
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          ...
```
{% endstep %}

{% step %}
## Get Wide Pod Information

```bash
kubectl get pods -o wide
```

The wide output adds information such as:

* Pod IP.
* Node.
* Nominated node.
* Readiness gates.

Example structure:

```
NAME          READY   STATUS    RESTARTS   AGE     IP              NODE
hello-world   1/1     Running   0          ...     172.17.x.x      10.241.x.x
```
{% endstep %}

{% step %}
## Describe the Pod

```bash
kubectl describe pod hello-world
```

This provides detailed information about the Pod and its Kubernetes state.
{% endstep %}

{% step %}
## Delete the Pod

```bash
kubectl delete pod hello-world
```

Verify that the namespace no longer contains the Pod:

```bash
kubectl get pods
```
{% endstep %}
{% endstepper %}

## Create a Pod with Imperative Object Configuration

This section demonstrates defining a complete Pod in a YAML file and then creating it with an imperative `kubectl` command.

### Pod Configuration: `hello-world-create.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world
spec:
  containers:
    - name: hello-world
      image: us.icr.io/sn-labs-x/hello-world:1
      ports:
        - containerPort: 8080
  imagePullSecrets:
    - name: icr
```

### Configuration Breakdown

| Field              | Purpose                                   |
| ------------------ | ----------------------------------------- |
| `apiVersion: v1`   | Uses the core Kubernetes API version      |
| `kind: Pod`        | Declares a Pod object                     |
| `metadata.name`    | Pod name: `hello-world`                   |
| `spec.containers`  | Defines the Pod container                 |
| `containers.name`  | Container name: `hello-world`             |
| `containers.image` | Image used by the container               |
| `containerPort`    | Application port exposed by the container |
| `imagePullSecrets` | Secret used to pull the private image     |

{% hint style="info" %}
The example uses `sn-labs-x` in the image path. In a real lab environment, use the namespace associated with your current account.
{% endhint %}

{% stepper %}
{% step %}
## Create the Pod from the YAML File

```bash
kubectl create -f hello-world-create.yaml
```

Expected result:

```
pod/hello-world created
```
{% endstep %}

{% step %}
## Verify the Pod

```bash
kubectl get pods
```

Expected structure:

```
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          ...
```
{% endstep %}

{% step %}
## Delete the Pod

```bash
kubectl delete pod hello-world
```

Expected result:

```
pod "hello-world" deleted
```
{% endstep %}

{% step %}
## Verify Deletion

```bash
kubectl get pods
```

The namespace should report no user-created resources.
{% endstep %}
{% endstepper %}

## Create a Workload with Declarative Configuration

This section moves from imperative object creation to declarative management.

Instead of directly telling Kubernetes which individual operations to perform, the configuration describes the desired state.

### Deployment Configuration: `hello-world-apply.yaml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  generation: 1
  labels:
    run: hello-world
  name: hello-world
spec:
  replicas: 3
  selector:
    matchLabels:
      run: hello-world
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        run: hello-world
    spec:
      containers:
        - image: us.icr.io/<my_namespace>/hello-world:1
          imagePullPolicy: Always
          name: hello-world
          ports:
            - containerPort: 8080
              protocol: TCP
          resources:
            limits:
              cpu: 2m
              memory: 30Mi
            requests:
              cpu: 1m
              memory: 10Mi
      imagePullSecrets:
        - name: icr
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      securityContext: {}
      terminationGracePeriodSeconds: 30
```

### Deployment Configuration Breakdown

| Configuration                       | Purpose                                   |
| ----------------------------------- | ----------------------------------------- |
| `apiVersion: apps/v1`               | Deployment API version                    |
| `kind: Deployment`                  | Declares a Deployment                     |
| `metadata.name`                     | Deployment name                           |
| `metadata.labels`                   | Adds a label to the Deployment            |
| `replicas: 3`                       | Desired number of Pod replicas            |
| `selector.matchLabels`              | Identifies Pods managed by the Deployment |
| `strategy.type: RollingUpdate`      | Uses rolling update behavior              |
| `maxSurge: 1`                       | Allows one extra Pod during rollout       |
| `maxUnavailable: 1`                 | Allows one unavailable Pod during rollout |
| `template.metadata.labels`          | Labels Pods created by the Deployment     |
| `containers.image`                  | Image used by Pods                        |
| `imagePullPolicy: Always`           | Always attempt to pull the image          |
| `containerPort: 8080`               | Application port                          |
| `resources.limits`                  | Maximum CPU and memory values             |
| `resources.requests`                | Requested CPU and memory values           |
| `imagePullSecrets`                  | Registry authentication                   |
| `dnsPolicy: ClusterFirst`           | Default cluster DNS policy                |
| `restartPolicy: Always`             | Restart containers when needed            |
| `terminationGracePeriodSeconds: 30` | Grace period before forced termination    |

{% stepper %}
{% step %}
## Apply the Desired State

```bash
kubectl apply -f hello-world-apply.yaml
```

Expected result:

```
deployment.apps/hello-world created
```

The configuration file is treated as the desired state for the Deployment.
{% endstep %}

{% step %}
## Verify the Deployment

```bash
kubectl get deployments
```

Example:

```
NAME          READY   UP-TO-DATE   AVAILABLE   AGE
hello-world   3/3     3            3           ...
```

This indicates that:

* Three replicas are ready.
* Three replicas are up to date.
* Three replicas are available.
{% endstep %}

{% step %}
## Verify the Three Pods

```bash
kubectl get pods
```

Example structure:

```
NAME                           READY   STATUS    RESTARTS   AGE
hello-world-...                1/1     Running   0          ...
hello-world-...                1/1     Running   0          ...
hello-world-...                1/1     Running   0          ...
```

The exact generated Pod names vary.
{% endstep %}

{% step %}
## Delete One Pod and Observe Replacement

Delete one of the current Pods:

```bash
kubectl delete pod hello-world-5d7cc94cb5-npdtg && \
kubectl get pods
```

The important behavior is:

1. One Pod is deleted.
2. The Deployment/ReplicaSet detects that the desired replica count is no longer satisfied.
3. A replacement Pod is created automatically.
4. The application returns to three replicas.

Example progression:

```
Before:
Pod A
Pod B
Pod C

Delete Pod A
   ↓
Pod B
Pod C

Controller reconciliation
   ↓
New Pod D

After:
Pod B
Pod C
Pod D
```

This demonstrates Kubernetes reconciliation and self-healing through the Deployment/ReplicaSet relationship.
{% endstep %}
{% endstepper %}

## Load Balancing the Application

The final section demonstrates Kubernetes Service-based access and load balancing across the three application replicas.

### Application Code: `app.js`

```javascript
var express = require('express');
var os = require('os');
var hostname = os.hostname();
var app = express();

app.get('/', function (req, res) {
  res.send('Hello world, ' + hostname + '! Your app is up and running!\n');
});

app.listen(8080, function () {
  console.log('Sample app is listening on port 8080.');
});
```

### What the Application Does

The application:

* Uses Express.
* Obtains the container hostname using Node's `os` module.
* Listens on port `8080`.
* Returns the hostname in the HTTP response.

This makes it possible to see which Pod handled a request.

## Dockerfile for the Application

```dockerfile
FROM node:9.4.0-alpine
COPY app.js .
COPY package.json .
RUN npm install &&\
    apk update &&\
    apk upgrade
EXPOSE 8080
CMD node app.js
```

### Dockerfile Breakdown

| Instruction              | Purpose                            |
| ------------------------ | ---------------------------------- |
| `FROM node:9.4.0-alpine` | Base image                         |
| `COPY app.js .`          | Copies application code            |
| `COPY package.json .`    | Copies Node package metadata       |
| `RUN npm install`        | Installs dependencies              |
| `RUN apk update`         | Updates Alpine package metadata    |
| `RUN apk upgrade`        | Upgrades installed Alpine packages |
| `EXPOSE 8080`            | Documents application port         |
| `CMD node app.js`        | Starts the Node application        |

## Expose the Deployment as a Service

{% stepper %}
{% step %}
## Create the Service

```bash
kubectl expose deployment/hello-world
```

This creates a Service for the Deployment.
{% endstep %}

{% step %}
## Verify the Service

```bash
kubectl get services
```

Example output:

```
NAME          TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
hello-world   ClusterIP   172.21.142.190   <none>        8080/TCP   ...
```

Important information:

* Service name: `hello-world`
* Service type: `ClusterIP`
* Service port: `8080/TCP`
{% endstep %}

{% step %}
## Create a Local Kubernetes Proxy

```bash
kubectl proxy
```

Expected message:

```
Starting to serve on 127.0.0.1:8001
```

The local proxy makes the cluster API and Service available through the local machine.
{% endstep %}

{% step %}
## Test the Application Through the Service

```bash
curl -L localhost:8001/api/v1/namespaces/sn-labs-$USERNAME/services/hello-world/proxy
```

Example response:

```
Hello world, hello-world-...! Your app is up and running!
```

The hostname identifies the Pod that processed the request.
{% endstep %}

{% step %}
## Observe Load Balancing Across Replicas

Run the request repeatedly:

```bash
for i in `seq 10`; do \
  curl -L localhost:8001/api/v1/namespaces/sn-labs-$USERNAME/services/hello-world/proxy; \
done
```

Different requests can be served by different replicas.

Example response pattern:

```
Hello world, hello-world-...-pskk6! Your app is up and running!
Hello world, hello-world-...-pskk6! Your app is up and running!
Hello world, hello-world-...-xn2tp! Your app is up and running!
Hello world, hello-world-...-pskk6! Your app is up and running!
Hello world, hello-world-...-xn2tp! Your app is up and running!
Hello world, hello-world-...-rks8g! Your app is up and running!
...
```

The exact Pod names are generated by Kubernetes and can differ.

```
Client request
      ↓
Kubernetes Service
      ↓
Load balancing
  ┌───┼───┐
  ↓   ↓   ↓
 Pod  Pod  Pod
  A    B    C
```

Requests can reach different application replicas.
{% endstep %}

{% step %}
## Clean Up the Lab

Delete the Deployment and Service together:

```bash
kubectl delete deployment/hello-world service/hello-world
```

Expected results:

```
deployment.apps "hello-world" deleted
service "hello-world" deleted
```
{% endstep %}
{% endstepper %}

## Complete Command Reference

| Command                                     | Purpose                                            |
| ------------------------------------------- | -------------------------------------------------- |
| `kubectl version`                           | Check client and server Kubernetes versions        |
| `git clone ...`                             | Obtain the CC201 course repository                 |
| `ls`                                        | List files in the working directory                |
| `kubectl config get-clusters`               | List configured clusters                           |
| `kubectl config get-contexts`               | List kubeconfig contexts                           |
| `kubectl get pods`                          | List Pods                                          |
| `export MY_NAMESPACE=...`                   | Store the lab namespace in an environment variable |
| `docker build -t ... .`                     | Build the application image                        |
| `docker push ...`                           | Push the image to IBM Cloud Container Registry     |
| `kubectl run ...`                           | Create a Pod imperatively                          |
| `kubectl get pods -o wide`                  | Show extended Pod information                      |
| `kubectl describe pod ...`                  | Inspect a Pod in detail                            |
| `kubectl delete pod ...`                    | Delete a Pod                                       |
| `kubectl create -f ...`                     | Create a resource from YAML                        |
| `kubectl apply -f ...`                      | Apply desired-state configuration                  |
| `kubectl get deployments`                   | Inspect Deployments                                |
| `kubectl expose deployment/...`             | Create a Service for a Deployment                  |
| `kubectl get services`                      | Inspect Services                                   |
| `kubectl proxy`                             | Start a local proxy to the Kubernetes API          |
| `curl -L ...`                               | Request the application through the Service proxy  |
| `kubectl delete deployment/... service/...` | Delete the lab Deployment and Service              |

## All Commands — Copy/Paste Reference

### Environment

```bash
kubectl version

[ ! -d 'CC201' ] && git clone \
  https://github.com/ibm-developer-skills-network/CC201.git

ls
```

### Cluster Context

```bash
kubectl config get-clusters
kubectl config get-contexts
kubectl get pods
```

### Imperative Pod

```bash
export MY_NAMESPACE=sn-labs-$USERNAME

docker build -t us.icr.io/$MY_NAMESPACE/hello-world:1 . && \
docker push us.icr.io/$MY_NAMESPACE/hello-world:1

kubectl run hello-world \
  --image us.icr.io/$MY_NAMESPACE/hello-world:1 \
  --overrides='{"spec":{"template":{"spec":{"imagePullSecrets":[{"name":"icr"}]}}}}'

kubectl get pods
kubectl get pods -o wide
kubectl describe pod hello-world
kubectl delete pod hello-world
kubectl get pods
```

### Imperative Object Configuration

```bash
kubectl create -f hello-world-create.yaml
kubectl get pods
kubectl delete pod hello-world
kubectl get pods
```

### Declarative Configuration

```bash
kubectl apply -f hello-world-apply.yaml
kubectl get deployments
kubectl get pods
```

### Reconciliation Demonstration

```bash
kubectl delete pod <one-of-the-hello-world-pods> && kubectl get pods
```

### Service and Load Balancing

```bash
kubectl expose deployment/hello-world
kubectl get services
kubectl proxy
curl -L localhost:8001/api/v1/namespaces/sn-labs-$USERNAME/services/hello-world/proxy
```

### Repeated Load-Balancing Requests

```bash
for i in `seq 10`; do \
  curl -L localhost:8001/api/v1/namespaces/sn-labs-$USERNAME/services/hello-world/proxy; \
done
```

### Cleanup

```bash
kubectl delete deployment/hello-world service/hello-world
```

## YAML Reference — Imperative Pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-world
spec:
  containers:
    - name: hello-world
      image: us.icr.io/sn-labs-x/hello-world:1
      ports:
        - containerPort: 8080
  imagePullSecrets:
    - name: icr
```

## YAML Reference — Declarative Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  generation: 1
  labels:
    run: hello-world
  name: hello-world
spec:
  replicas: 3
  selector:
    matchLabels:
      run: hello-world
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        run: hello-world
    spec:
      containers:
        - image: us.icr.io/<my_namespace>/hello-world:1
          imagePullPolicy: Always
          name: hello-world
          ports:
            - containerPort: 8080
              protocol: TCP
          resources:
            limits:
              cpu: 2m
              memory: 30Mi
            requests:
              cpu: 1m
              memory: 10Mi
      imagePullSecrets:
        - name: icr
      dnsPolicy: ClusterFirst
      restartPolicy: Always
      securityContext: {}
      terminationGracePeriodSeconds: 30
```

## Node / Pod / Deployment / Service Relationship

```
Deployment
    |
    +---- ReplicaSet
            |
            +---- Pod 1 ----+
            |              |
            +---- Pod 2 ----+---- Application
            |              |
            +---- Pod 3 ----+
                    |
                    v
                 Service
                    |
                    v
               Client requests
```

## Imperative vs. Imperative-Configuration vs. Declarative

| Approach                  | User provides           | Kubernetes provides                         |
| ------------------------- | ----------------------- | ------------------------------------------- |
| Imperative command        | Explicit operation      | Performs requested operation                |
| Imperative configuration  | Operation + object file | Creates/updates requested object            |
| Declarative configuration | Desired state           | Determines and performs required operations |

### Imperative

```
User
  ↓
Command
  ↓
Operation
  ↓
Kubernetes
```

### Imperative Object Configuration

```
User
  ↓
Operation + YAML/JSON
  ↓
Kubernetes
```

### Declarative

```
User
  ↓
Desired-state YAML
  ↓
kubectl apply
  ↓
Kubernetes determines required actions
  ↓
Actual cluster state
```

## Load Balancing Demonstration

```
                    Client
                      |
                      v
                 Kubernetes
                  Service
                      |
            +---------+---------+
            |         |         |
            v         v         v
         Pod A     Pod B     Pod C
          |           |          |
       hostname    hostname   hostname
            \         |         /
             \        |        /
              Application replicas
```

By requesting the same Service repeatedly, responses can come from different Pod hostnames, demonstrating that Kubernetes distributes traffic across the replicas.

## Expected Learning Outcomes

After completing the lab, you should have practiced:

* Using `kubectl`.
* Checking cluster/context configuration.
* Creating a Pod imperatively.
* Creating a Pod from a YAML file.
* Applying a declarative Deployment configuration.
* Running multiple replicas.
* Observing Kubernetes reconciliation after a Pod is deleted.
* Creating a Service.
* Using `kubectl proxy`.
* Calling a Service with `curl`.
* Observing requests reach different replicas.
* Cleaning up Kubernetes resources.

## Lab Flow — End to End

```
Verify Kubernetes
      ↓
Configure / inspect context
      ↓
Build + push hello-world image
      ↓
Create Pod imperatively
      ↓
Inspect Pod
      ↓
Delete Pod
      ↓
Create Pod with YAML
      ↓
Inspect and delete Pod
      ↓
Create 3-replica Deployment declaratively
      ↓
Inspect Deployment
      ↓
Inspect Pods
      ↓
Delete one Pod
      ↓
Observe automatic replacement
      ↓
Expose Deployment as Service
      ↓
Run kubectl proxy
      ↓
curl Service endpoint
      ↓
Repeat requests
      ↓
Observe different Pod hostnames
      ↓
Delete Deployment + Service
```

## Reference

* Coursera course: `https://www.coursera.org/learn/ibm-containers-docker-kubernetes-openshift`
* IBM Developer Skills Network CC201 repository: `https://github.com/ibm-developer-skills-network/CC201`

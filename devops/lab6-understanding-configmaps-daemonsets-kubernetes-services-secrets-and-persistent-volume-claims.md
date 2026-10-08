# Lab6 - Understanding ConfigMaps, DaemonSets, Kubernetes Services, Secrets & Persistent Volume Claims

<div align="left"><img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBM-DB0110EN-SkillsNetwork/images/IBM_logo.png" alt="" width="300"></div>

**Estimated time needed:** 1 hour

In this lab, you will build and deploy an application to Kubernetes, then understand and create ConfigMaps, DaemonSets, Kubernetes Services, Secrets, and further explore Volumes & Persistent Volume Claims.

#### Objectives

In this Practice Project, you will build and deploy a JavaScript application to Kubernetes using Docker.\
You will understand and create the following:

* ConfigMap
* DaemonSet
* Kubernetes Service
* Secret
* Volumes and Persistent Volume Claims

## About the Dockerfile

1. Clone the repository containing the starter code to begin the project.

```bash
git clone https://github.com/ibm-developer-skills-network/containers-project.git
```

2. Open the `Dockerfile` located in the main project directory.

<div align="left"><img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/d1XFIic-VBupmjaZFaTz_A/dockerfile-location.png" alt="dockerfile-location.png"></div>

3. It's content will be as follows:

```yml
# Use an official Node.js runtime as a parent image
FROM node:14

# Set the working directory in the container
WORKDIR /app

# Copy the application files to the working directory
COPY main.js .
COPY public/index.html public/index.html
COPY public/style.css public/style.css

# Make port 3000 available to the world outside this container
EXPOSE 3000

# Run the application when the container launches
CMD ["node", "main.js"]
```

**Here is an explanation of the code in it:**

1. `FROM node:14` specifies the base image to be used, which is an official Node.js runtime version 14.
2. `WORKDIR /app` sets the working directory inside the container to /app.
3. `COPY main.js .` copies main.js from the host to the current directory (.) in the container.
4. `COPY public/index.html public/index.html` copies index.html from the public directory on the host to the public directory in the container.
5. `COPY public/style.css public/style.css` copies style.css from the public directory on the host to the public directory in the container.
6. `EXPOSE 3000` exposes port 3000 of the container to allow connections from the outside.
7. `CMD ["node", "main.js"]` specifies the command to run when the container launches, which is to execute node main.js.

## Build and deploy the application to Kubernetes

The repository already has the code for the application as you have observed in the earlier section. We are just going to build the docker image and push to the registry.

You will be giving the name `myapp` to your Kubernetes deployed application.

1. Navigate to the project directory.

```bash
 cd containers-project/
```

2. Export your namespace.

```bash
export MY_NAMESPACE=sn-labs-$USERNAME 
```

3. Build the Docker image.

```bash
docker build . -t us.icr.io/$MY_NAMESPACE/myapp:v1 
```

![docker-build.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/PNF9ntiqz_8iu1G-tFA4bA/docker-build.png)

4. Push the tagged image to the IBM Cloud container registry.

```bash
docker push us.icr.io/$MY_NAMESPACE/myapp:v1
```

![docker-push.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/hYgYyyuCEWVDQZkeMzOKZQ/docker-push.png)

5. List all the images available. You will see the newly created `myapp` image.

```bash
ibmcloud cr images
```

![myapp-img-created.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/M44p1OL9vf42GE5cg3lgYQ/myapp-img-created.png)

6. Open the `deployment.yml` file located in the main project directory. It's content will be as follows:

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: myapp
  strategy:
    rollingUpdate:
      maxSurge: 25%
      maxUnavailable: 25%
    type: RollingUpdate
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
      - image: us.icr.io/<your SN labs namespace>/myapp:v1
        imagePullPolicy: Always
        name: myapp
        ports:
        - containerPort: 3000
          name: http
        resources:
          limits:
            cpu: 50m
          requests:
            cpu: 20m
```

**Here is an explanation of the code within it.**

* `apiVersion`: apps/v1 specifies the version of the Kubernetes API being used and the resource type (Deployment).
* `kind`: Deployment indicates that this YAML defines a Deployment object.
* `metadata` section includes metadata about the Deployment, such as its name and labels.
* `spec` section defines the desired state for the Deployment, including the number of replicas, update strategy, and pod template.
* `replicas`: 1 specifies that there should be one replica of the application running.
* `selector` defines how the Deployment finds which Pods to manage, using labels.
* `strategy` specifies the update strategy for the Deployment, here using rolling updates with certain constraints.
* `template` describes the Pod template used for creating new Pods.
* `containers` lists the containers within the Pod.
* `image` specifies the Docker image to use for the container.
* `imagePullPolicy`: Always ensures that the latest image is always pulled from the registry.
* `name` assigns a name to the container.
* `ports` section specifies which ports should be exposed by the container.
* `resources` defines resource requests and limits for the container, such as CPU.

7. Replace `<your SN labs namespace>` with your actual SN labs namespace.

<details>

<summary>Click here for the ways to get your namespace</summary>

1. Run the command `oc project`, and use the namespace mapped to your project name

![getting-namespace-1.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/BiMuagMmxx-Yo-MCyjbzPw/getting-namespace-1.png)

2. Run the command `ibmcloud cr namespaces` and use the one which shows your sn-labs-username

![getting-namespace-2.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/DLfzjAKNhvVNvL3FzONIMw/getting-namespace-2.png)

</details>

8. Apply the deployment.

```bash
kubectl apply -f deployment.yml
```

![apply-deploymnet.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/SPFOjn4DnlYpaNjryRieWw/apply-deploymnet.png)

9. Verify that the application pods are running and accessible.

```bash
kubectl get pods
```

![myapp-deployment--get-pods.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/hEGm94YIl_e9hDIduHUgeA/myapp-deployment--get-pods.png)

10. Start the application on port-forward:

```bash
kubectl port-forward deployment.apps/myapp 3000:3000 
```

![port-fwd\_running.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/hFyKY_wEoa7XL_zubH2cAw/port-fwd-running.png)\
11\. Launch the app on Port `3000` to view the application output.

12. You should see the message `Hello from MyApp. Your app is up!`.\
    ![deployed\_myapp\_output.png](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/AsxbJI7blrRy1ol6EbMJuQ/deployed-myapp-output.png)
13. Stop the server before proceeding further, by pressing `CTRL + C`.

<br>

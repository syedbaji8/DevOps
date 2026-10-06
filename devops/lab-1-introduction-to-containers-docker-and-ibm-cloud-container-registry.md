# Lab-1: Introduction to Containers, Docker, and IBM Cloud Container Registry

## Introduction to Containers, Docker, and IBM Cloud Container Registry

<div align="left"><img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/images/IDSN-logo.png" alt="cognitiveclass.ai logo" width="200"></div>

### Objectives

In this lab, you will:

* Pull an image from Docker Hub
* Run an image as a container using `d&#8203;ocker`
* Build an image using a Dockerfile
* Push an image to IBM Cloud Container Registry

> > **Note: Kindly complete the lab in a single session without any break because the lab may go on offline mode and may cause errors. If you face any issues/errors during the lab process, please logout from the lab environment. Then clear your system cache and cookies and try to complete the lab.**

**Important:** You may already have an IBM Cloud account and may even have a namespace in the IBM Container Registry (ICR). However, in this lab **you will not be using your own IBM Cloud account or your own ICR namespace**. You will be using an IBM Cloud account that has been automatically generated for you for this excercise. The lab environment will _not_ have access to any resources within your personal IBM Cloud account, including ICR namespaces and images.

## Verify the environment and command line tools

1.  Open a terminal window by using the menu in the editor: `Terminal > New Terminal`.

    > > **Note:If the terminal is already opened, please skip this step.**

<img src="https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/env&#x26;cmdlinetools_1.png" alt="" width="800">

2. Verify that `d&#8203;ocker` CLI is installed.

```
docker --version    
```

You should see the following output, although the version may be different:

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/NwAp7u-gtWzCv2mpDBAGuw/docker%20version.png)

3. Verify that `ibmcloud` CLI is installed.

```
ibmcloud version
```

You should see the following output, although the version may be different:

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/Hd3JkpCQJ5Iub-SoTu3uIw/ibm%20cloud%20version.png)

4.  Change to your project folder.

    > > **Note: If you are already on the ‘/home/project’ folder, please skip this step.**

```
cd /home/project
```

5. Clone the git repository that contains the artifacts needed for this lab, if it doesn’t already exist.

```
[ ! -d 'CC201' ] && git clone https://github.com/ibm-developer-skills-network/CC201.git
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/tBzfenQsY5HYJZZujgGdIw/git%20clone.png)

6. Change to the directory for this lab by running the following command. `c&#8203;d` will change the working/current directory to the directory with the name specified, in this case **CC201/labs/1\_ContainersAndDcoker**.

```
cd CC201/labs/1_ContainersAndDocker/
```

7. List the contents of this directory to see the artifacts for this lab.

```
ls
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/env\&cmdlinetools_6.png)

## Pull an image from Docker Hub and run it as a container

1. Use the `d&#8203;ocker` CLI to list your images.

```
docker images        
```

You should see an empty table (with only headings) since you don’t have any images yet.

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/pullimg_ctr_1.png)

2. Pull your first image from Docker Hub.

```
docker pull hello-world        
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/pullimg_ctr_2.png)

3. List images again.

```
docker images
```

You should now see the `hello-world` image present in the table.

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/pullimg_ctr_3.png)

4. Run the `hello-world` image as a container.

```
docker run hello-world
```

You should see a **‘Hello from Docker!’** message.

There will also be an explanation of what Docker did to generate this message.

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/pullimg_ctr_4.png)

5. List the containers to see that your container ran and exited successfully.

```
docker ps -a
```

Among other things, for this container you should see a container ID, the image name (`hello-world`), and a status that indicates that the container exited successfully.

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/gx887uavxN9VR6x_M-BaKA/docker%20ps%20a.png)

6. Note the CONTAINER ID from the previous output and replace the tag in the command below with this value. This command removes your container.

```
docker container rm <container_id>
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/pullimg_ctr_6.png)

7. Verify that that the container has been removed. Run the following command.

```
docker ps -a
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/pullimg_ctr_7.png)

Congratulations on pulling an image from Docker Hub and running your first container! Now let’s try and build our own image.

## Build an image using a Dockerfile

1. The current working directory contains a simple Node.js application that we will run in a container. The app will print a hello message along with the hostname. The following files are needed to run the app in a container:

* app.js is the main application, which simply replies with a hello world message.
* package.json defines the dependencies of the application.
* Dockerfile defines the instructions Docker uses to build the image.

2. Use the Explorer to view the files needed for this app. Click the Explorer icon (it looks like a sheet of paper) on the left side of the window, and then navigate to the directory for this lab: `CC201 > labs > 1_ContainersAndDocker`. Click `Dockerfile` to view the commands required to build an image.

![Dockerfile in Explorer](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/dockerfile-explorer.png)

> > **You can refresh your understanding of the commands mentioned in the Dockerfile below:**\
> > The FROM instruction initializes a new build stage and specifies the base image that subsequent instructions will build upon.\
> > The COPY command enables us to copy files to our image.\
> > The RUN instruction executes commands.\
> > The EXPOSE instruction exposes a particular port with a specified protocol inside a Docker Container.\
> > The CMD instruction provides a default for executing a container, or in other words, an executable that should run in your container.

3. Run the following command to build the image:

```
docker build . -t myimage:v1
```

As seen in the module videos, the output creates a new layer for each instruction in the Dockerfile.

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/xldzex3L-0y1aaxucaOCAg/docker%20build.png)

4. List images to see your image tagged `myimage:v1` in the table.

```
docker images        
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/TFGiUNfvbxNPbL4Npoqqnw/docker%20images.png)

Note that compared to the `hello-world` image, this image has a different image ID. This means that the two images consist of different layers – in other words, they’re not the same image.

## Run the image as a container

1. Now that your image is built, run it as a container with the following command:

```
docker run -dp 8080:8080 myimage:v1        
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/run_img_as_detached_ctr_3.png)

The output is a unique code allocated by docker for the application you are running.

2. Run the `curl` command to ping the application as given below.

```
curl localhost:8080
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/run_img_as_ctr_3.png)

If you see the output as above, it indicates that **‘Your app is up and running!’.**

3. Now to stop the container we use `d&#8203;ocker stop` followed by the container id. The following command uses `d&#8203;ocker ps -q` to pass in the list of all running containers:

```
docker stop $(docker ps -q)
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/run_img_as_ctr_4.png)

4. Check if the container has stopped by running the following command.

```
docker ps
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/run_img_as_ctr_5.png)

## Push the image to IBM Cloud Container Registry

1. The environment should have already logged you into the IBM Cloud account that has been automatically generated for you by the Skills Network Labs environment. The following command will give you information about the account you’re targeting:

```
ibmcloud target
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_1.png)

2. The environment also created an IBM Cloud Container Registry (ICR) namespace for you. Since Container Registry is multi-tenant, namespaces are used to divide the registry among several users. Use the following command to see the namespaces you have access to:

```
ibmcloud cr namespaces        
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_2.png)

You should see two namespaces listed starting with `sn-labs`:

* The first one with your username is a namespace just for you. You have full _read_ and _write_ access to this namespace.
* The second namespace, which is a shared namespace, provides you with only Read Access

3. Ensure that you are targeting the region appropriate to your cloud account, for instance `us-south` region where these namespaces reside as you saw in the output of the `ibmcloud target` command.

```
ibmcloud cr region-set us-south
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_3.png)

4. Log your local Docker daemon into IBM Cloud Container Registry so that you can push to and pull from the registry.

```
ibmcloud cr login
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/ntTWaLTC7h_ajrho18rz4w/ibmcloud%20cr%20login.png)

5. Export your namespace as an environment variable so that it can be used in subsequent commands.

```
export MY_NAMESPACE=sn-labs-$USERNAME
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_5.png)

6. Tag your image so that it can be pushed to IBM Cloud Container Registry.

```
docker tag myimage:v1 us.icr.io/$MY_NAMESPACE/hello-world:1
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_6.png)

7. Push the newly tagged image to IBM Cloud Container Registry.

```
docker push us.icr.io/$MY_NAMESPACE/hello-world:1
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_7.png)

> **Note:** If you have tried this lab earlier, there might be a possibility that the previous session is still persistent. In such a case, you will see a **‘Layer already Exists’** message instead of the **‘Pushed’** message in the above output. We recommend you to proceed with the next steps of the lab.

8. Verify that the image was successfully pushed by listing images in Container Registry.

```
ibmcloud cr images
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_8.png)

Optionally, to only view images within a specific namespace.

```
ibmcloud cr images --restrict $MY_NAMESPACE
```

![](https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/cc201/labs/1_ContainersAndDocker/images/push_img_9.png)

You should see your image name in the output.

Congratulations! You have completed the first lab for the first module of this course.

#### © IBM Corporation. All rights reserved.



| Command                         | Description                                                                  |
| ------------------------------- | ---------------------------------------------------------------------------- |
| **curl localhost description**  | Pings the application.                                                       |
| **docker build**                | Builds an image from a Dockerfile.                                           |
| **docker build . -t**           | Builds the image and tags the image id.                                      |
| **docker container rm**         | Removes a container.                                                         |
| **docker images**               | Lists the images.                                                            |
| **docker ps**                   | Lists the containers.                                                        |
| **docker ps -a description**    | Lists the containers that ran and exited successfully.                       |
| **docker pull**                 | Pulls the latest image or repository from a registry.                        |
| **docker push**                 | Pushes an image or a repository to a registry.                               |
| **docker run**                  | Runs a command in a new container.                                           |
| **docker run -p**               | Runs the container by publishing the ports.                                  |
| **docker stop**                 | Stops one or more running containers.                                        |
| **docker stop $(docker ps -q)** | Stops all running containers.                                                |
| **docker tag**                  | Creates a tag for a target image that refers to a source image.              |
| **docker --version**            | Displays the version of the Docker CLI.                                      |
| **exit**                        | Closes the terminal session.                                                 |
| **export MY\_NAMESPACE**        | Exports a namespace as an environment variable.                              |
| **git clone**                   | Clones the git repository that contains the artifacts needed.                |
| **ibmcloud cr images**          | Lists images in the IBM Cloud Container Registry.                            |
| **ibmcloud cr login**           | Logs your local Docker daemon into IBM Cloud Container Registry.             |
| **ibmcloud cr namespaces**      | Views the namespaces you have access to.                                     |
| **ibmcloud cr region-set**      | Ensures that you are targeting the region appropriate to your cloud account. |
| **ibmcloud target**             | Provides information about the account you’re targeting.                     |
| **ibmcloud version**            | Displays the version of the IBM Cloud CLI.                                   |
| **ls**                          | Lists the contents of this directory to see the artifacts.                   |



## Container Basics

| Term                                    | Definition                                                                                                                                                                                                                                                                                                                                                                                                    |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Agile**                               | is an iterative approach to project management and software development that helps teams deliver value to their customers faster and with fewer issues.                                                                                                                                                                                                                                                       |
| **Client-server architecture**          | is a distributed application structure that partitions tasks or workloads between the providers of a resource or service, called servers, and service requesters, called clients.                                                                                                                                                                                                                             |
| **A container**                         | powered by the containerization engine, is a standard unit of software that encapsulates the application code, runtime, system tools, system libraries, and settings necessary for programmers to efficiently build, ship and run applications.                                                                                                                                                               |
| **Container Registry**                  | Used for the storage and distribution of named container images. While many features can be built on top of a registry, its most basic functions are to store images and retrieve them.                                                                                                                                                                                                                       |
| **CI/CD pipelines**                     | A continuous integration and continuous deployment (CI/CD) pipeline is a series of steps that must be performed in order to deliver a new version of software. CI/CD pipelines are a practice focused on improving software delivery throughout the software development life cycle via automation.                                                                                                           |
| **Cloud native**                        | A cloud-native application is a program that is designed for a cloud computing architecture. These applications are run and hosted in the cloud and are designed to capitalize on the inherent characteristics of a cloud computing software delivery model.                                                                                                                                                  |
| **Daemon-less**                         | A container runtime that does not run any specific program (daemon) to create objects, such as images, containers, networks, and volumes.                                                                                                                                                                                                                                                                     |
| **DevOps**                              | is a set of practices, tools, and a cultural philosophy that automate and integrate the processes between software development and IT teams.                                                                                                                                                                                                                                                                  |
| **Docker**                              | An open container platform for developing, shipping and running applications in containers.                                                                                                                                                                                                                                                                                                                   |
| **A Dockerfile**                        | is a text document that contains all the commands you would normally execute manually in order to build a Docker image. Docker can build images automatically by reading the instructions from a Dockerfile.                                                                                                                                                                                                  |
| **Docker client**                       | is the primary way that many Docker users interact with Docker. When you use commands such as docker run, the client sends these commands to dockerd, which carries them out. The docker command uses the Docker API. The Docker client can communicate with more than one daemon.                                                                                                                            |
| **Docker Command Line Interface (CLI)** | The Docker client provides a command line interface (CLI) that allows you to issue build, run, and stop application commands to a Docker daemon.                                                                                                                                                                                                                                                              |
| **Docker daemon (dockerd)**             | creates and manages Docker objects, such as images, containers, networks, and volumes.                                                                                                                                                                                                                                                                                                                        |
| **Docker Hub**                          | is the world's easiest way to create, manage, and deliver your team's container applications.                                                                                                                                                                                                                                                                                                                 |
| **Docker localhost**                    | Docker provides a host network which lets containers share your host's networking stack. This approach means that a localhost in a container resolves to the physical host, instead of the container itself.                                                                                                                                                                                                  |
| **Docker remote host**                  | A remote Docker host is a machine, inside or outside our local network which is running a Docker Engine and has ports exposed for querying the Engine API.                                                                                                                                                                                                                                                    |
| **Docker networks**                     | help isolate container communications.                                                                                                                                                                                                                                                                                                                                                                        |
| **Docker plugins**                      | such as a storage plugin, provides the ability to connect external storage platforms.                                                                                                                                                                                                                                                                                                                         |
| **Docker storage**                      | uses volumes and bind mounts to persist data even after a running container is stopped.                                                                                                                                                                                                                                                                                                                       |
| **LXC**                                 | LinuX Containers is a OS-level virtualization technology that allows creation and running of multiple isolated Linux virtual environments (VE) on a single control host.                                                                                                                                                                                                                                      |
| **IBM Cloud Container Registry**        | stores and distributes container images in a fully managed private registry.                                                                                                                                                                                                                                                                                                                                  |
| **Image**                               | An immutable file that contains the source code, libraries, and dependencies that are necessary for an application to run. Images are templates or blueprints for a container.                                                                                                                                                                                                                                |
| **Immutability**                        | Images are read-only; if you change an image, you create a new image.                                                                                                                                                                                                                                                                                                                                         |
| **Microservices**                       | are a cloud-native architectural approach in which a single application contains many loosely coupled and independently deployable smaller components or services.                                                                                                                                                                                                                                            |
| **Namespace**                           | A Linux namespace is a Linux kernel feature that isolates and virtualizes system resources. Processes which are restricted to a namespace can only interact with resources or processes that are part of the same namespace. Namespaces are an important part of Docker's isolation model. Namespaces exist for each type of resource, including networking, storage, processes, hostname control and others. |
| **Operating System Virtualization**     | OS-level virtualization is an operating system paradigm in which the kernel allows the existence of multiple isolated user space instances, called containers, zones, virtual private servers, partitions, virtual environments, virtual kernels, or jails.                                                                                                                                                   |
| **Private Registry**                    | Restricts access to images so that only authorized users can view and use them.                                                                                                                                                                                                                                                                                                                               |
| **REST API**                            | A REST API (also known as RESTful API) is an application programming interface (API or web API) that conforms to the constraints of REST architectural style and allows for interaction with RESTful web services.                                                                                                                                                                                            |
| **Registry**                            | is a hosted service containing repositories of images which responds to the Registry API.                                                                                                                                                                                                                                                                                                                     |
| **Repository**                          | is a set of Docker images. A repository can be shared by pushing it to a registry server. The different images in the repository can be labelled using tags.                                                                                                                                                                                                                                                  |
| **Server Virtualization**               | Server virtualization is the process of dividing a physical server into multiple unique and isolated virtual servers by means of a software application. Each virtual server can run its own operating systems independently.                                                                                                                                                                                 |
| **Serverless**                          | is a cloud-native development model that allows developers to build and run applications without having to manage servers.                                                                                                                                                                                                                                                                                    |
| **Tag**                                 | A tag is a label applied to a Docker image in a repository. Tags are how various images in a repository are distinguished from each other.                                                                                                                                                                                                                                                                    |

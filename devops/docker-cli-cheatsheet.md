# Docker CLI Cheatsheet

<figure><img src="../.gitbook/assets/Docker CLI Cheatsheet Mind Map.png" alt=""><figcaption></figcaption></figure>

## Cheat Sheet: Docker CLI

### Source and Scope

This document is a structured Markdown version of the **Cheat Sheet: Docker CLI** reading linked from the supplied Coursera page:

`https://www.coursera.org/learn/ibm-containers-docker-kubernetes-openshift/supplement/wBjIF/cheat-sheet-docker-cli`

#### Source verification

The individual Coursera supplement page is accessible, but its reading body is not exposed in the browser extraction. The command/description content below was therefore reconstructed from a publicly accessible copy titled **Docker Cheatsheet Ibm**, which reproduces the same one-page “Cheat Sheet: Docker CLI” table. The public copy contains the command list and descriptions shown below. citeturn396121view0turn396121search1

The broader Coursera course page confirms that **Cheat Sheet: Docker CLI** is a Module 1 reading in **Containers and Containerization**, listed as approximately **5 minutes**. The module covers Docker CLI usage, Dockerfile commands, image naming, networking, storage, plugins, and related container workflows. citeturn911991search0

> **Fidelity note:** Command names and descriptions are preserved from the accessible cheat-sheet copy. No additional Docker commands have been added to the source table.

***

## 1. Cheat Sheet Purpose

The Docker CLI cheat sheet is a quick reference for commonly used commands associated with:

* Docker images.
* Docker containers.
* Docker registries.
* IBM Cloud Container Registry.
* Git repositories.
* Shell/environment utilities.
* Terminal sessions.

***

## 2. Docker CLI Commands

| Command                       | Description                                                     |
| ----------------------------- | --------------------------------------------------------------- |
| `curl localhost`              | Pings the application.                                          |
| `docker build`                | Builds an image from a Dockerfile.                              |
| `docker build . -t`           | Builds the image and tags the image ID.                         |
| `docker CLI`                  | Starts the Docker command line interface.                       |
| `docker container rm`         | Removes a container.                                            |
| `docker images`               | Lists the images.                                               |
| `docker ps`                   | Lists the containers.                                           |
| `docker ps -a`                | Lists the containers that ran and exited successfully.          |
| `docker pull`                 | Pulls the latest image or repository from a registry.           |
| `docker push`                 | Pushes an image or a repository to a registry.                  |
| `docker run`                  | Runs a command in a new container.                              |
| `docker run -p`               | Runs the container by publishing the ports.                     |
| `docker stop`                 | Stops one or more running containers.                           |
| `docker stop $(docker ps -q)` | Stops all running containers.                                   |
| `docker tag`                  | Creates a tag for a target image that refers to a source image. |
| `docker --version`            | Displays the version of the Docker CLI.                         |

***

## 3. `curl`

```bash
curl localhost
```

**Purpose:** Pings the application.

***

## 4. `docker build`

```bash
docker build
```

**Purpose:** Builds an image from a Dockerfile.

***

## 5. Building and Tagging an Image

The source lists:

```bash
docker build . -t
```

**Purpose:** Builds the image and tags the image ID.

> The source entry does not provide the completed tag value after `-t`, so no missing argument is invented here.

***

## 6. Docker CLI

```
docker CLI
```

**Purpose:** Starts the Docker command line interface.

***

## 7. Removing a Container

```bash
docker container rm
```

**Purpose:** Removes a container.

***

## 8. Listing Images

```bash
docker images
```

**Purpose:** Lists the images.

***

## 9. Listing Running Containers

```bash
docker ps
```

**Purpose:** Lists the containers.

***

## 10. Listing Containers That Have Exited

```bash
docker ps -a
```

**Purpose:** Lists the containers that ran and exited successfully.

***

## 11. Pulling Images from a Registry

```bash
docker pull
```

**Purpose:** Pulls the latest image or repository from a registry.

***

## 12. Pushing Images to a Registry

```bash
docker push
```

**Purpose:** Pushes an image or a repository to a registry.

***

## 13. Running a Container

```bash
docker run
```

**Purpose:** Runs a command in a new container.

***

## 14. Publishing Container Ports

```bash
docker run -p
```

**Purpose:** Runs the container by publishing the ports.

***

## 15. Stopping Containers

```bash
docker stop
```

**Purpose:** Stops one or more running containers.

***

## 16. Stopping All Running Containers

```bash
docker stop $(docker ps -q)
```

**Purpose:** Stops all running containers.

***

## 17. Tagging Images

```bash
docker tag
```

**Purpose:** Creates a tag for a target image that refers to a source image.

***

## 18. Checking the Docker CLI Version

```bash
docker --version
```

**Purpose:** Displays the version of the Docker CLI.

***

## 19. Shell and Environment Commands

| Command               | Description                                                   |
| --------------------- | ------------------------------------------------------------- |
| `exit`                | Closes the terminal session.                                  |
| `export MY_NAMESPACE` | Exports a namespace as an environment variable.               |
| `git clone`           | Clones the Git repository that contains the artifacts needed. |
| `ls`                  | Lists the contents of this directory to see the artifacts.    |

### `exit`

```bash
exit
```

Closes the terminal session.

### `export MY_NAMESPACE`

```bash
export MY_NAMESPACE
```

Exports a namespace as an environment variable.

### `git clone`

```bash
git clone
```

Clones the Git repository that contains the artifacts needed.

### `ls`

```bash
ls
```

Lists the contents of this directory to see the artifacts.

***

## 20. IBM Cloud Container Registry Commands

| Command                  | Description                                                                  |
| ------------------------ | ---------------------------------------------------------------------------- |
| `ibmcloud cr images`     | Lists images in the IBM Cloud Container Registry.                            |
| `ibmcloud cr login`      | Logs your local Docker daemon into IBM Cloud Container Registry.             |
| `ibmcloud cr namespaces` | Views the namespaces you have access to.                                     |
| `ibmcloud cr region-set` | Ensures that you are targeting the region appropriate to your cloud account. |

### `ibmcloud cr images`

```bash
ibmcloud cr images
```

Lists images in the IBM Cloud Container Registry.

### `ibmcloud cr login`

```bash
ibmcloud cr login
```

Logs your local Docker daemon into IBM Cloud Container Registry.

### `ibmcloud cr namespaces`

```bash
ibmcloud cr namespaces
```

Views the namespaces you have access to.

### `ibmcloud cr region-set`

```bash
ibmcloud cr region-set
```

Ensures that you are targeting the region appropriate to your cloud account.

***

## 21. IBM Cloud CLI Commands

| Command            | Description                                              |
| ------------------ | -------------------------------------------------------- |
| `ibmcloud target`  | Provides information about the account you’re targeting. |
| `ibmcloud version` | Displays the version of the IBM Cloud CLI.               |

### `ibmcloud target`

```bash
ibmcloud target
```

Provides information about the account you’re targeting.

### `ibmcloud version`

```bash
ibmcloud version
```

Displays the version of the IBM Cloud CLI.

***

## 22. Complete Cheat Sheet Table

| Category                | Command                       | Purpose                                                        |
| ----------------------- | ----------------------------- | -------------------------------------------------------------- |
| Application test        | `curl localhost`              | Pings the application                                          |
| Docker image            | `docker build`                | Builds an image from a Dockerfile                              |
| Docker image            | `docker build . -t`           | Builds the image and tags the image ID                         |
| Docker CLI              | `docker CLI`                  | Starts the Docker command line interface                       |
| Containers              | `docker container rm`         | Removes a container                                            |
| Images                  | `docker images`               | Lists the images                                               |
| Containers              | `docker ps`                   | Lists the containers                                           |
| Containers              | `docker ps -a`                | Lists containers that ran and exited successfully              |
| Registry                | `docker pull`                 | Pulls the latest image or repository from a registry           |
| Registry                | `docker push`                 | Pushes an image or repository to a registry                    |
| Containers              | `docker run`                  | Runs a command in a new container                              |
| Containers / networking | `docker run -p`               | Runs the container by publishing the ports                     |
| Containers              | `docker stop`                 | Stops one or more running containers                           |
| Containers              | `docker stop $(docker ps -q)` | Stops all running containers                                   |
| Images                  | `docker tag`                  | Creates a tag for a target image referring to a source image   |
| Docker CLI              | `docker --version`            | Displays the Docker CLI version                                |
| Shell                   | `exit`                        | Closes the terminal session                                    |
| Environment             | `export MY_NAMESPACE`         | Exports a namespace as an environment variable                 |
| Git                     | `git clone`                   | Clones the Git repository containing needed artifacts          |
| IBM Cloud Registry      | `ibmcloud cr images`          | Lists images in IBM Cloud Container Registry                   |
| IBM Cloud Registry      | `ibmcloud cr login`           | Logs the local Docker daemon into IBM Cloud Container Registry |
| IBM Cloud Registry      | `ibmcloud cr namespaces`      | Views accessible namespaces                                    |
| IBM Cloud Registry      | `ibmcloud cr region-set`      | Sets the appropriate IBM Cloud Registry region                 |
| IBM Cloud               | `ibmcloud target`             | Provides information about the targeted account                |
| IBM Cloud CLI           | `ibmcloud version`            | Displays the IBM Cloud CLI version                             |
| Shell                   | `ls`                          | Lists directory contents/artifacts                             |

***

## 23. All Commands — Copy/Paste Reference

```bash
curl localhost

docker build

docker build . -t

docker CLI

docker container rm

docker images

docker ps

docker ps -a

docker pull

docker push

docker run

docker run -p

docker stop
docker stop $(docker ps -q)
docker tag
docker --version
exit
export MY_NAMESPACE
git clone
ibmcloud cr images
ibmcloud cr login
ibmcloud cr namespaces
ibmcloud cr region-set
ibmcloud target
ibmcloud version
ls
```

***

## 24. Docker Image Workflow Referenced by the Cheat Sheet

```
Dockerfile
    ↓
docker build
    ↓
Docker image
    ↓
docker tag
    ↓
docker push
    ↓
Registry
    ↓
docker pull
    ↓
Local image
    ↓
docker run
    ↓
Running container
```

***

## 25. Container Management Workflow

```
docker ps
   ↓
Identify containers
   ↓
docker container rm
   ↓
Remove a container
```

Or:

```
docker stop
   ↓
Stop running containers
```

For all running containers:

```bash
docker stop $(docker ps -q)
```

***

## 26. Docker Networking / Port Publishing

The cheat sheet specifically includes:

```bash
docker run -p
```

The source description says this runs the container by publishing the ports.

The source does not provide concrete host-port/container-port values after `-p`.

***

## 27. IBM Cloud Container Registry Workflow

The registry commands can be organized as:

```
IBM Cloud account
      ↓
ibmcloud target
      ↓
ibmcloud cr region-set
      ↓
ibmcloud cr login
      ↓
ibmcloud cr namespaces
      ↓
ibmcloud cr images
```

The source provides the purpose of each command but does not provide complete argument values.

***

## 28. Git and Local Artifacts

The cheat sheet includes:

```bash
git clone
```

and:

```bash
ls
```

The source describes these as:

* Cloning the Git repository containing the needed artifacts.
* Listing directory contents to see the artifacts.

***

## 29. Docker CLI Quick Mental Model

```
BUILD
  docker build
      ↓
TAG
  docker tag
      ↓
PUSH
  docker push
      ↓
REGISTRY
      ↓
PULL
  docker pull
      ↓
RUN
  docker run
      ↓
CONTAINER
      ↓
PS / STOP / RM
```

***

## 30. Command Categories

### Image Management

```bash
docker build
docker build . -t
docker images
docker pull
docker push
docker tag
```

### Container Management

```bash
docker container rm
docker ps
docker ps -a
docker run
docker run -p
docker stop
docker stop $(docker ps -q)
```

### Docker CLI

```bash
docker CLI
docker --version
```

### Shell / Environment

```bash
exit
export MY_NAMESPACE
ls
```

### Source Control

```bash
git clone
```

### IBM Cloud Container Registry

```bash
ibmcloud cr images
ibmcloud cr login
ibmcloud cr namespaces
ibmcloud cr region-set
```

### IBM Cloud Account / CLI

```bash
ibmcloud target
ibmcloud version
```

### Application Testing

```bash
curl localhost
```

***

## 31. Source Fidelity Notes

The accessible source contains the following command entries exactly as presented:

```
docker build . -t
docker CLI
docker –version
export MY_NAMESPACE
```

The first entry does not include a completed tag value after `-t`, and `export MY_NAMESPACE` is shown without a concrete value. The source also renders the Docker version command with a typographic dash in one occurrence. This document preserves the source spelling in the notes above while using the standard ASCII form below for an executable command block:

```bash
docker --version
```

No missing arguments have been invented.

***

## 32. Course Context

The Coursera course places this cheat sheet in **Module 1 — Containers and Containerization**. The course describes Module 1 as covering Docker fundamentals, Docker CLI usage, Docker objects, Dockerfile instructions, container image naming, Docker networking, storage, plugins, image pulling/running/building/tagging, and pushing images to a registry. citeturn911991search0

The course page lists **Cheat Sheet: Docker CLI** as a reading of approximately **5 minutes**. citeturn911991search0

***

## 33. Complete Source Table

The accessible copy presents the cheat sheet as a one-page two-column table headed **Command** and **Description**. The complete content is represented below in the same command/description structure.

| Command                       | Description                                                                  |
| ----------------------------- | ---------------------------------------------------------------------------- |
| `curl localhost`              | Pings the application.                                                       |
| `docker build`                | Builds an image from a Dockerfile.                                           |
| `docker build . -t`           | Builds the image and tags the image id.                                      |
| `docker CLI`                  | Start the Docker command line interface.                                     |
| `docker container rm`         | Removes a container.                                                         |
| `docker images`               | Lists the images.                                                            |
| `docker ps`                   | Lists the containers.                                                        |
| `docker ps -a`                | Lists the containers that ran and exited successfully.                       |
| `docker pull`                 | Pulls the latest image or repository from a registry.                        |
| `docker push`                 | Pushes an image or a repository to a registry.                               |
| `docker run`                  | Runs a command in a new container.                                           |
| `docker run -p`               | Runs the container by publishing the ports.                                  |
| `docker stop`                 | Stops one or more running containers.                                        |
| `docker stop $(docker ps -q)` | Stops all running containers.                                                |
| `docker tag`                  | Creates a tag for a target image that refers to a source image.              |
| `docker --version`            | Displays the version of the Docker CLI.                                      |
| `exit`                        | Closes the terminal session.                                                 |
| `export MY_NAMESPACE`         | Exports a namespace as an environment variable.                              |
| `git clone`                   | Clones the git repository that contains the artifacts needed.                |
| `ibmcloud cr images`          | Lists images in the IBM Cloud Container Registry.                            |
| `ibmcloud cr login`           | Logs your local Docker daemon into IBM Cloud Container Registry.             |
| `ibmcloud cr namespaces`      | Views the namespaces you have access to.                                     |
| `ibmcloud cr region-set`      | Ensures that you are targeting the region appropriate to your cloud account. |
| `ibmcloud target`             | Provides information about the account you’re targeting.                     |
| `ibmcloud version`            | Displays the version of the IBM Cloud CLI.                                   |
| `ls`                          | Lists the contents of this directory to see the artifacts.                   |

***

## 34. Source Limitation

The direct Coursera supplement page was successfully located, but its reading body was not exposed by the browser extractor. The individual command/description content was therefore recovered from an accessible public copy that reproduces the one-page cheat sheet. The Coursera course page independently confirms the reading title and Module 1 placement. citeturn396121view2turn911991search0

No images were added because the source is a command-reference sheet and the command tables/code blocks provide a clearer and more useful Markdown representation than decorative imagery.

***

## Source References

1. Coursera — **Cheat Sheet: Docker CLI**\
   https://www.coursera.org/learn/ibm-containers-docker-kubernetes-openshift/supplement/wBjIF/cheat-sheet-docker-cli
2. Coursera — **Introduction to Containers w/ Docker, Kubernetes & OpenShift**\
   https://www.coursera.org/learn/ibm-containers-docker-kubernetes-openshift
3. Accessible public copy used to recover the cheat-sheet table: **Docker Cheatsheet Ibm**. citeturn396121view0

***

## 35. Real-Time Usage Guide

The original cheat sheet is a reference list. This section adds **practical real-world usage examples** so you can understand when and why you would run each command.

> **Important distinction:** The command descriptions and original entries above are source-derived. The examples in this section are practical examples based on current Docker and IBM Cloud CLI documentation and common development workflows. They are added to make the cheat sheet usable in real projects. Current Docker documentation confirms the command forms for image building, running containers, listing images/containers, tagging, pulling, pushing, stopping, removing, authentication, and version inspection. citeturn187425search4turn711455search1turn187425search0turn834208search2turn834208search1turn711455search2turn924205search4turn711455search4turn711455search6turn834208search0turn711455search0

***

## 36. Real-Time Scenario: Run an Nginx Website Locally

This is the easiest way to understand the Docker workflow.

### Step 1 — Check Docker

```bash
docker --version
```

**When you use it:** When joining a new machine or troubleshooting whether Docker CLI is installed.

The Docker documentation distinguishes `docker --version` (CLI version) from `docker version` (client/server version information). citeturn711455search0

***

### Step 2 — Download an Image

```bash
docker pull nginx:alpine
```

**When you use it:** When the image you want is not already available locally.

Docker's current documentation describes `docker pull` as downloading an image from a registry; if a tag is omitted, Docker uses `latest` by default. citeturn711455search4

***

### Step 3 — Check the Image

```bash
docker images
```

**When you use it:** After `docker pull` or `docker build`, to verify that the image exists locally.

The current Docker documentation says `docker images` lists local images, including repository, tag, image ID, creation time, and size. citeturn187425search0

***

### Step 4 — Run the Container

```bash
docker run --name web -d nginx:alpine
```

**What happens:**

```
nginx:alpine image
        ↓
docker run
        ↓
Container named "web"
        ↓
Container runs in background
```

`docker run` creates and runs a new container from an image. Docker's current syntax is:

```
docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

The `--name` option gives the container an easy-to-remember name. citeturn711455search1

***

### Step 5 — Check the Running Container

```bash
docker ps
```

**When you use it:** To answer, “What containers are running right now?”

The current docs state that `docker ps` shows running containers by default. citeturn834208search2

***

### Step 6 — Publish a Port

If you want to open nginx from your browser, map a host port to the container port:

```bash
docker stop web
docker rm web

docker run --name web -d -p 8080:80 nginx:alpine
```

Now open:

```
http://localhost:8080
```

#### What `-p 8080:80` means

```
Your PC
localhost:8080
      │
      ▼
Docker
      │
      ▼
Container port 80
      │
      ▼
Nginx
```

Docker's official Dockerfile documentation demonstrates the same host-to-container port publishing pattern with `docker run -p`. citeturn187425search4

***

### Step 7 — Test with curl

```bash
curl localhost:8080
```

**When you use it:** When you want to verify the application from the terminal instead of opening a browser.

This is the practical version of the cheat sheet's:

```bash
curl localhost
```

***

## 37. Real-Time Scenario: Build Your Own Application Image

Imagine you have this project:

```
my-app/
├── Dockerfile
├── package.json
├── package-lock.json
└── server.js
```

Your Dockerfile might be:

```dockerfile
FROM node:22-alpine

WORKDIR /app

COPY package*.json ./
RUN npm ci

COPY . .

EXPOSE 3000

CMD ["node", "server.js"]
```

### Step 1 — Build the Image

The original cheat sheet lists:

```bash
docker build
```

For a real build, you normally give the image a name and tag:

```bash
docker build -t my-app:1.0 .
```

Here:

| Part            | Meaning                                        |
| --------------- | ---------------------------------------------- |
| `docker build`  | Build an image                                 |
| `-t my-app:1.0` | Give the image a repository/name and tag       |
| `.`             | Use the current directory as the build context |

Docker's current documentation shows the `-t name:tag` pattern and explains that `.` is the build context. citeturn187425search4turn924205search5

***

### Step 2 — Verify the Image

```bash
docker images
```

Look for:

```
my-app    1.0
```

***

### Step 3 — Run Your Application

```bash
docker run --name my-app-container -d -p 3000:3000 my-app:1.0
```

Then test:

```bash
curl localhost:3000
```

Or open:

```
http://localhost:3000
```

***

## 38. Real-Time Scenario: See What Is Running

Suppose you are debugging a development machine and don't know what Docker is currently running.

Start with:

```bash
docker ps
```

This shows running containers.

Then:

```bash
docker ps -a
```

This shows both running and stopped containers. Docker documents `-a/--all` as the option that includes stopped containers. citeturn834208search2

#### Practical debugging flow

```
Something is not working
        ↓
docker ps
        ↓
Is the container running?
        ↓
No?
        ↓
docker ps -a
        ↓
What happened to the container?
```

***

## 39. Real-Time Scenario: Stop a Container

```bash
docker stop my-app-container
```

**When you use it:** When you want the application to stop gracefully.

Docker's current documentation says `docker stop` stops one or more running containers; by default the main process receives `SIGTERM`, followed by `SIGKILL` after the configured grace period if needed. citeturn711455search2

***

## 40. Real-Time Scenario: Remove a Container

After stopping it:

```bash
docker rm my-app-container
```

**When you use it:** When you no longer need that container.

Docker's current documentation describes `docker container rm` / `docker rm` as removing one or more containers. citeturn834208search1

#### Common lifecycle

```
docker run
    ↓
Running container
    ↓
docker stop
    ↓
Stopped container
    ↓
docker rm
    ↓
Container removed
```

***

## 41. Real-Time Scenario: Stop All Running Containers

The source cheat sheet provides:

```bash
docker stop $(docker ps -q)
```

**When you use it:** When you intentionally want to stop every currently running Docker container.

#### Important

This is a shell command that uses command substitution. It is most natural in Bash-like shells.

Before running it in a shared development machine, check:

```bash
docker ps
```

because it can stop multiple unrelated containers.

***

## 42. Real-Time Scenario: Tag an Image for a Registry

Suppose you built:

```bash
docker build -t my-app:1.0 .
```

You want to push it to Docker Hub under your repository.

Tag it:

```bash
docker tag my-app:1.0 <dockerhub-username>/my-app:1.0
```

Now you have:

```
my-app:1.0
        ↓
<dockerhub-username>/my-app:1.0
```

Docker's current documentation defines `docker image tag` as creating a new target reference for an existing source image. citeturn924205search4

***

## 43. Real-Time Scenario: Login to a Registry

Before pushing to a private or authenticated registry:

```bash
docker login
```

For a self-hosted registry:

```bash
docker login registry.example.com
```

Docker's current documentation describes `docker login` as authenticating to a registry and notes that authentication may be required for pushing and pulling private images. citeturn834208search0

***

## 44. Real-Time Scenario: Push an Image

After tagging:

```bash
docker push <dockerhub-username>/my-app:1.0
```

**When you use it:** When you want another developer, server, CI/CD pipeline, or Kubernetes cluster to pull your image.

Docker's current documentation describes `docker push` as uploading an image to a registry. citeturn711455search6

#### Typical workflow

```
Code
 ↓
docker build
 ↓
Local image
 ↓
docker tag
 ↓
docker login
 ↓
docker push
 ↓
Registry
```

***

## 45. Real-Time Scenario: Pull the Image on Another Machine

On another machine:

```bash
docker pull <dockerhub-username>/my-app:1.0
```

Then:

```bash
docker run --name my-app -d -p 3000:3000 <dockerhub-username>/my-app:1.0
```

This is a very common team workflow:

```
Developer A
    ↓
Build
    ↓
Push
    ↓
Registry
    ↓
Developer B / Server / CI / Kubernetes
    ↓
Pull
    ↓
Run
```

***

## 46. Real-Time Scenario: Inspect Image Tags

Suppose you have several versions:

```
my-app:1.0
my-app:1.1
my-app:2.0
```

Use:

```bash
docker images my-app
```

or:

```bash
docker images
```

The current Docker documentation supports filtering the image listing by repository and tag. citeturn187425search0

***

## 47. Real-Time Scenario: Export an IBM Cloud Namespace

The source cheat sheet lists:

```bash
export MY_NAMESPACE
```

In a real Bash-like shell, you would assign a value:

```bash
export MY_NAMESPACE=sn-labs-yourname
```

Then:

```bash
echo $MY_NAMESPACE
```

The idea is:

```
Environment variable
        ↓
MY_NAMESPACE
        ↓
Reuse in Docker / registry commands
```

***

## 48. Real-Time IBM Cloud Container Registry Workflow

The original cheat sheet includes:

```bash
ibmcloud cr images
ibmcloud cr login
ibmcloud cr namespaces
ibmcloud cr region-set
```

The current IBM Cloud documentation uses the longer command names `image-list` and `namespace-list`, while `images` and `namespaces` are aliases. citeturn924205search0

### Step 1 — Log in to IBM Cloud

Current IBM Cloud setup documentation requires an IBM Cloud CLI login before working with the registry:

```bash
ibmcloud login
```

### Step 2 — Install the Container Registry Plugin

If necessary:

```bash
ibmcloud plugin install container-registry
```

IBM's current documentation identifies the `container-registry` plugin as the CLI component used to manage namespaces and images. citeturn924205search2

### Step 3 — Check the Target Account

```bash
ibmcloud target
```

**Real-time use:** Confirm which IBM Cloud account/project/resource group your CLI is targeting.

### Step 4 — Select a Registry Region

Example:

```bash
ibmcloud cr region-set us-south
```

IBM's current documentation uses `us-south` as an example region. citeturn924205search0

### Step 5 — List Namespaces

Source form:

```bash
ibmcloud cr namespaces
```

Current documented form:

```bash
ibmcloud cr namespace-list
```

The current docs identify `namespaces` as the alias for `namespace-list`. citeturn924205search0

### Step 6 — Log Docker into IBM Cloud Container Registry

```bash
ibmcloud cr login
```

This authenticates the local Docker/Podman client with IBM Cloud Container Registry and is required for registry push/pull operations. citeturn924205search0turn924205search3

### Step 7 — List Images

Source form:

```bash
ibmcloud cr images
```

Current documented form:

```bash
ibmcloud cr image-list
```

`images` is an alias for `image-list`. citeturn924205search0

***

## 49. Real-Time IBM Cloud Image Workflow

```
ibmcloud login
       ↓
ibmcloud plugin install container-registry
       ↓
ibmcloud target
       ↓
ibmcloud cr region-set us-south
       ↓
ibmcloud cr namespace-list
       ↓
ibmcloud cr login
       ↓
docker build
       ↓
docker tag
       ↓
docker push
       ↓
IBM Cloud Container Registry
```

***

## 50. Real-Time Example: Push an Application to IBM Cloud Container Registry

Suppose:

```
Application name: my-app
Version: 1.0
Namespace: mynamespace
Region: us-south
```

Build:

```bash
docker build -t my-app:1.0 .
```

Tag for IBM Cloud Container Registry:

```bash
docker tag my-app:1.0 us.icr.io/mynamespace/my-app:1.0
```

Authenticate:

```bash
ibmcloud cr login
```

Push:

```bash
docker push us.icr.io/mynamespace/my-app:1.0
```

List images:

```bash
ibmcloud cr image-list --restrict mynamespace
```

This is a realistic enterprise workflow for moving a locally built image into a private registry. IBM's current Container Registry documentation confirms the `ibmcloud cr login` prerequisite and the `image-list`/namespace workflow. citeturn924205search0turn924205search3

***

## 51. Real-Time Scenario: `curl localhost`

The source cheat sheet uses:

```bash
curl localhost
```

In practice, the application must first be listening on the expected host port.

Example:

```bash
docker run --name web -d -p 8080:80 nginx:alpine
```

Then:

```bash
curl localhost:8080
```

This creates a complete relationship:

```
curl
 ↓
localhost:8080
 ↓
Docker host port 8080
 ↓
Container port 80
 ↓
Nginx
```

***

## 52. Real-Time Scenario: `ls`

```bash
ls
```

**When you use it:** When working inside a project directory and you want to confirm that files such as these are present:

```
Dockerfile
package.json
src/
README.md
```

Typical sequence:

```bash
cd my-app
ls
docker build -t my-app:1.0 .
```

***

## 53. Real-Time Scenario: `git clone`

The source cheat sheet says `git clone` clones the repository containing needed artifacts.

A real example is:

```bash
git clone https://github.com/example/my-app.git
cd my-app
ls
```

Then:

```bash
docker build -t my-app:1.0 .
```

The overall developer workflow becomes:

```
Git repository
    ↓
git clone
    ↓
Project files
    ↓
Dockerfile
    ↓
docker build
    ↓
Image
```

***

## 54. Real-Time Scenario: `exit`

```bash
exit
```

Use it when you want to:

* Leave a shell session.
* Close a terminal session.
* Exit an interactive shell.

For example:

```
Inside terminal
    ↓
exit
    ↓
Back to previous shell/session
```

***

## 55. What You Would Actually Do During a Frontend/Full-Stack Project

A very common workflow could look like this:

### 1. Pull the code

```bash
git clone https://github.com/example/my-app.git
cd my-app
```

### 2. Check project files

```bash
ls
```

### 3. Build the Docker image

```bash
docker build -t my-app:1.0 .
```

### 4. Check the image

```bash
docker images my-app
```

### 5. Run locally

```bash
docker run --name my-app-container -d -p 3000:3000 my-app:1.0
```

### 6. Test the application

```bash
curl localhost:3000
```

### 7. Check the container

```bash
docker ps
```

### 8. Stop it when finished

```bash
docker stop my-app-container
```

### 9. Remove it

```bash
docker rm my-app-container
```

### 10. Publish it for other environments

```bash
docker tag my-app:1.0 <registry-user>/my-app:1.0
docker login
docker push <registry-user>/my-app:1.0
```

This is the practical Docker lifecycle:

```
Code
 ↓
Build
 ↓
Image
 ↓
Run
 ↓
Test
 ↓
Stop
 ↓
Remove
 ↓
Tag
 ↓
Push
 ↓
Registry
```

***

## 56. Real-Time Troubleshooting Flow

When a Docker application is not working:

```
Is Docker installed?
        ↓
docker --version
        ↓
Does the image exist?
        ↓
docker images
        ↓
Is the container running?
        ↓
docker ps
        ↓
Was it created but stopped?
        ↓
docker ps -a
        ↓
Check port publishing
        ↓
docker ps
        ↓
Test localhost
        ↓
curl localhost:<port>
```

For a stopped container:

```bash
docker ps -a
```

For a container that should be removed:

```bash
docker rm <container-name>
```

For a running container that should be stopped:

```bash
docker stop <container-name>
```

Docker's current CLI documentation supports this `ps` → stop/remove workflow. citeturn834208search2turn711455search2turn834208search1

***

## 57. Interview-Friendly Explanation of the Docker Workflow

You can explain the commands in an interview like this:

> “In a typical Docker workflow, I first build an image using `docker build`. I can verify it with `docker images`. Then I run the image using `docker run`, often publishing a port with `-p` so I can access the application from my browser or using curl. I use `docker ps` to check running containers and `docker ps -a` to see stopped containers. When I finish, I use `docker stop` and `docker rm`. If the image needs to be shared with a team or deployed to another environment, I tag it with `docker tag`, authenticate with the registry, and push it using `docker push`. On another machine, I can use `docker pull` and run the image there.”

***

## 58. Most Important Commands to Practice First

For practical Docker work, focus first on these:

| Priority | Command                                         | What you should understand      |
| -------: | ----------------------------------------------- | ------------------------------- |
|        1 | `docker build -t app:1.0 .`                     | Build an image                  |
|        2 | `docker images`                                 | See local images                |
|        3 | `docker run -d --name app -p 3000:3000 app:1.0` | Run and expose an application   |
|        4 | `docker ps`                                     | See running containers          |
|        5 | `docker ps -a`                                  | See all containers              |
|        6 | `docker stop app`                               | Stop a container                |
|        7 | `docker rm app`                                 | Remove a container              |
|        8 | `docker tag`                                    | Prepare an image for a registry |
|        9 | `docker login`                                  | Authenticate                    |
|       10 | `docker push`                                   | Upload image                    |
|       11 | `docker pull`                                   | Download image                  |

***

## 59. Updated Practical Command Cheat Sheet

```bash
# Check Docker CLI
docker --version

# Build
docker build -t my-app:1.0 .

# List images
docker images

# Run
docker run --name my-app -d my-app:1.0

# Run and publish a port
docker run --name my-app -d -p 3000:3000 my-app:1.0

# List running containers
docker ps

# List all containers
docker ps -a

# Stop a container
docker stop my-app

# Remove a container
docker rm my-app

# Tag an image
docker tag my-app:1.0 username/my-app:1.0

# Login to a registry
docker login

# Push
docker push username/my-app:1.0

# Pull
docker pull username/my-app:1.0

# Check application
curl localhost:3000
```

***

## 60. Important Difference: Image vs Container

A practical way to remember the commands:

```
IMAGE
  ↓
docker pull / docker build / docker tag / docker push
  ↓
CONTAINER
  ↓
docker run / docker ps / docker stop / docker rm
```

#### Image commands

```bash
docker build
docker images
docker pull
docker push
docker tag
```

#### Container commands

```bash
docker run
docker ps
docker ps -a
docker stop
docker container rm
```

***

## 61. Official Documentation References Used for Practical Examples

The practical syntax in this added section was checked against the current official documentation:

* Docker CLI overview\
  https://docs.docker.com/reference/cli/docker/ citeturn711455search3
* Docker build\
  https://docs.docker.com/reference/cli/docker/image/build/ citeturn924205search5
* Docker run\
  https://docs.docker.com/reference/cli/docker/run/ citeturn711455search1
* Docker images\
  https://docs.docker.com/reference/cli/docker/image/ls/ citeturn187425search0
* Docker ps\
  https://docs.docker.com/reference/cli/docker/container/ls/ citeturn834208search2
* Docker stop\
  https://docs.docker.com/reference/cli/docker/container/stop/ citeturn711455search2
* Docker rm\
  https://docs.docker.com/reference/cli/docker/container/rm/ citeturn834208search1
* Docker pull\
  https://docs.docker.com/reference/cli/docker/image/pull/ citeturn711455search4
* Docker push\
  https://docs.docker.com/reference/cli/docker/image/push/ citeturn711455search6
* Docker tag\
  https://docs.docker.com/reference/cli/docker/image/tag/ citeturn924205search4
* Docker login\
  https://docs.docker.com/reference/cli/docker/login/ citeturn834208search0
* Docker version\
  https://docs.docker.com/reference/cli/docker/version/ citeturn711455search0
* IBM Cloud Container Registry CLI\
  https://cloud.ibm.com/docs/Registry?topic=Registry-containerregcli citeturn924205search0
* IBM Cloud Container Registry setup\
  https://cloud.ibm.com/docs/Registry?topic=Registry-registry\_setup\_cli\_namespace citeturn924205search2

***

## 62. Final Practical Mental Model

```
1. GET THE CODE
   git clone
       ↓
2. CHECK FILES
   ls
       ↓
3. BUILD IMAGE
   docker build -t app:1.0 .
       ↓
4. VERIFY IMAGE
   docker images
       ↓
5. RUN CONTAINER
   docker run -d --name app -p 3000:3000 app:1.0
       ↓
6. TEST
   curl localhost:3000
       ↓
7. CHECK CONTAINER
   docker ps
       ↓
8. STOP
   docker stop app
       ↓
9. REMOVE
   docker rm app
       ↓
10. TAG
    docker tag app:1.0 registry-user/app:1.0
       ↓
11. LOGIN
    docker login
       ↓
12. PUSH
    docker push registry-user/app:1.0
       ↓
13. ANOTHER MACHINE
    docker pull registry-user/app:1.0
       ↓
14. RUN AGAIN
    docker run ...
```

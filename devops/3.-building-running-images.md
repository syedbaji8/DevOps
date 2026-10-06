# Building Running Images

<figure><img src="../.gitbook/assets/Docker Container Building Running Images Mind Map.png" alt=""><figcaption></figcaption></figure>

## Lesson Metadata

| Item                   | Details                                                          |
| ---------------------- | ---------------------------------------------------------------- |
| Course                 | **Introduction to Containers w/ Docker, Kubernetes & OpenShift** |
| Lesson                 | **Building and Running Container Images**                        |
| Listed lesson duration | **2:29**                                                         |
| Module                 | **Containers and Containerization**                              |

## Learning Objectives

After watching this lesson, you will be able to:

* Build a container image using a Dockerfile.
* Create a running container using an image.
* Describe key Docker commands.

## Development Process of a Running Container

```
Dockerfile
    ↓
Container Image
    ↓
Running Container
```

{% stepper %}
{% step %}
## Create a Dockerfile

Create a Dockerfile.
{% endstep %}

{% step %}
## Create a container image

Use the Dockerfile to create a container image.
{% endstep %}

{% step %}
## Create a running container

Use the container image to create a running container.
{% endstep %}
{% endstepper %}

## Dockerfile

The sample Dockerfile has the commands:

```dockerfile
FROM
CMD
```

### `FROM`

`FROM` defines the base image.

The source transcript does not specify the exact base image name used in the sample.

### `CMD`

`CMD` prints the words **hello world** on the terminal.

The source does not provide the exact `CMD` syntax.

```dockerfile
FROM <base image>
CMD <instruction that prints "hello world">
```

{% hint style="info" %}
The placeholders indicate information that the transcript describes but does not explicitly spell out. They are not presented as the exact Dockerfile from the video.
{% endhint %}

## Building the Container Image

The Docker command used to build the image uses:

* The `build` command.
* The tag.
* The repository.
* The version.
* The current directory.

```bash
docker build -t my-app:v1
```

The transcript does not provide the complete command-line syntax or the exact option characters used for the tag.

| Element           | Source information                |
| ----------------- | --------------------------------- |
| Docker command    | `build`                           |
| Tag               | Used during the build             |
| Repository        | Used for the resulting image name |
| Version           | Used as the image tag/version     |
| Current directory | Used as the build context         |

## Build Output and What It Confirms

After the build is run, the output messages include:

1. Sending build context to Docker Daemon.
2. `successfully built <image>`.
3. `successfully tagged my-app`.

| Build output                           | Meaning stated in the lesson                     |
| -------------------------------------- | ------------------------------------------------ |
| Sending build context to Docker Daemon | Build context is being sent to the Docker daemon |
| `successfully built <image>`           | Confirms image creation                          |
| `successfully tagged my-app`           | Confirms the image tag                           |

The container image was created and successfully tagged.

## Verifying the Container Image

To verify image creation, run the Docker `images` command:

```bash
docker images
```

The output displays:

* Repository.
* Tag.
* Image ID.
* Creation date.
* Image size.

| Image information | Example/value described in source |
| ----------------- | --------------------------------- |
| Repository        | `my-app`                          |
| Tag               | `v1`                              |
| Image ID          | Displayed in output               |
| Creation date     | Displayed in output               |
| Image size        | Displayed in output               |

## Creating and Running the Container

Create the container using the `run` command and the container image name and tag.

```bash
docker run my-app:v1
```

```
Container image name + tag
            ↓
        run command
            ↓
     Running container
            ↓
      "hello world"
```

The application prints:

```
hello world
```

## Viewing Details of the Created Container

Execute the Docker **PSA** command, which displays details of the container created.

```bash
docker ps -a
```

{% hint style="info" %}
The transcript says “Docker PSA command.” It does not provide a complete command-line form or spell out the intended options.
{% endhint %}

The source follows this with “Given the appropriate input,” but does not provide additional syntax.

## Key Docker Commands

| Command  | Purpose according to the lesson                             |
| -------- | ----------------------------------------------------------- |
| `build`  | Used to create container images with tags from a Dockerfile |
| `images` | Lists all images, their repositories, tags, and sizes       |
| `run`    | Creates and runs a container from an image                  |
| `push`   | Stores images in a configured registry                      |
| `pull`   | Retrieves images from a configured registry                 |

### `build`

> The build command is used to create container images with tags from a Dockerfile.

```bash
docker build -t my-app:v1 .
```

The build operation uses:

* Tag.
* Repository.
* Version.
* Current directory.

### `images`

> The images command will list all the images, their repositories and tags, and their sizes.

```bash
docker images
```

### `run`

> The run command creates and runs a container from an image.

```bash
docker run my-app:v1
```

### `push`

> The push command stores images in a configured registry.

```bash
docker push
```

The transcript does not provide the full argument syntax.

### `pull`

> The pull command retrieves images from a configured registry.

```bash
docker pull
```

The transcript does not provide the full argument syntax.

## Complete Command Reference

| Command         | Role               | Source-provided details                                                                                 | Exact full syntax in transcript?       |
| --------------- | ------------------ | ------------------------------------------------------------------------------------------------------- | -------------------------------------- |
| `docker build`  | Build image        | Creates tagged container images from a Dockerfile; uses tag, repository, version, and current directory | No                                     |
| `docker images` | Inspect images     | Lists images, repositories, tags, and sizes                                                             | Yes, command name is explicitly stated |
| `docker run`    | Run container      | Creates and runs a container from an image                                                              | No                                     |
| `docker push`   | Upload/store image | Stores images in a configured registry                                                                  | No                                     |
| `docker pull`   | Retrieve image     | Retrieves images from a configured registry                                                             | No                                     |

## End-to-End Workflow

{% stepper %}
{% step %}
## Create a Dockerfile

Create a Dockerfile.
{% endstep %}

{% step %}
## Define the base image

Define the base image with `FROM`.
{% endstep %}

{% step %}
## Define container startup behavior

Define the container startup behavior with `CMD`.
{% endstep %}

{% step %}
## Build the image

Build the image with the Docker `build` command.
{% endstep %}

{% step %}
## Tag the image

Tag the image.
{% endstep %}

{% step %}
## Confirm image creation

Confirm image creation from build output.
{% endstep %}

{% step %}
## Verify the image

Verify the image with `docker images`.
{% endstep %}

{% step %}
## Run the image

Run the image as a container.
{% endstep %}

{% step %}
## View application output

The application prints `hello world`.
{% endstep %}

{% step %}
## Display container details

Display details of the created container.
{% endstep %}

{% step %}
## Transfer images through a registry

Push images to a configured registry when needed and pull images from a configured registry when needed.
{% endstep %}
{% endstepper %}

## Dockerfile Concepts vs. Docker CLI Commands

| Category               | Items from the lesson |
| ---------------------- | --------------------- |
| Dockerfile instruction | `FROM`                |
| Dockerfile instruction | `CMD`                 |
| Docker CLI command     | `build`               |
| Docker CLI command     | `images`              |
| Docker CLI command     | `run`                 |
| Docker CLI command     | `push`                |
| Docker CLI command     | `pull`                |

## Image Concepts Mentioned

| Concept         | Lesson detail                        |
| --------------- | ------------------------------------ |
| Container image | Created from a Dockerfile            |
| Image tag       | Applied during the build             |
| Repository      | Part of the image naming information |
| Version         | Used in the image identification     |
| Image ID        | Displayed by `docker images`         |
| Creation date   | Displayed by `docker images`         |
| Image size      | Displayed by `docker images`         |
| Build context   | Sent to the Docker Daemon            |
| Registry        | Used by `push` and `pull`            |

```
Repository: my-app
Tag: v1
```

## Container Concepts Mentioned

* Creating a container from an image.
* Running a container from an image.
* Using an image name and tag when running a container.
* The application running inside the container.
* The application output being `hello world`.
* Viewing details of the created container.

```
Image
  ↓
Run
  ↓
Container
```

## Registry Concepts

### Push

The `push` command stores images in a configured registry:

```bash
docker push
```

### Pull

The `pull` command retrieves images from a configured registry:

```bash
docker pull
```

```
Local Image
    │
    └── push ──→ Configured Registry
                     │
                     └── pull ──→ Local Environment
```

## What You Learn

* The `build` command is used with a Dockerfile to build a container image.
* The `run` command is used with an image to create a running container.
* Key Docker commands covered include:
  * `build`
  * `images`
  * `run`
  * `pull`
  * `push`

> The run command is used with an image to create a running container and key.

## Source-Level Command Examples

{% tabs %}
{% tab title="Build" %}
```bash
docker build
```
{% endtab %}

{% tab title="List Images" %}
```bash
docker images
```
{% endtab %}

{% tab title="Run a Container" %}
```bash
docker run
```
{% endtab %}

{% tab title="Push an Image" %}
```bash
docker push
```
{% endtab %}

{% tab title="Pull an Image" %}
```bash
docker pull
```
{% endtab %}
{% endtabs %}

### Dockerfile Instructions

```dockerfile
FROM
CMD
```

## Information Explicitly Mentioned but Not Fully Specified

| Item                      | What the lesson specifies                                 | What is not specified        |
| ------------------------- | --------------------------------------------------------- | ---------------------------- |
| `FROM`                    | Defines the base image                                    | Exact base image             |
| `CMD`                     | Prints `hello world`                                      | Exact `CMD` syntax           |
| `docker build`            | Uses tag, repository, version, and current directory      | Complete command-line syntax |
| Image output              | Shows repository, tag, image ID, creation date, size      | Full sample output           |
| `docker run`              | Uses image name and tag; application prints `hello world` | Complete command-line syntax |
| Container-details command | Transcript calls it the “PSA” command                     | Exact syntax and options     |
| `docker push`             | Stores images in configured registry                      | Exact registry/image syntax  |
| `docker pull`             | Retrieves images from configured registry                 | Exact registry/image syntax  |

## Final Reference

### Learning Flow

```
Dockerfile
    ↓
FROM + CMD
    ↓
Build image
    ↓
Tag image
    ↓
Verify with docker images
    ↓
Run image
    ↓
Running container
    ↓
Application output: hello world
    ↓
Container details
    ↓
Push / Pull through configured registry
```

### Key Commands

```
build
images
run
push
pull
```

### Key Dockerfile Instructions

```
FROM
CMD
```

### Key Example Image Identity

```
my-app:v1
```

### Example Application Output

```
hello world
```

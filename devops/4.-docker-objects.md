# Docker Objects

<figure><img src="../.gitbook/assets/Docker Objects Infographic Mind Map.png" alt=""><figcaption></figcaption></figure>

After watching this lesson, you will be able to:

* Identify and describe Docker objects.
* Identify essential Dockerfile commands.
* Explain container image naming.
* Describe how Docker uses networks, storage, and plugins.

## Docker Objects

Docker contains objects such as:

| Docker object   | Description                                                                            |
| --------------- | -------------------------------------------------------------------------------------- |
| Dockerfile      | A text file containing instructions needed to create an image                          |
| Image           | A read-only template with instructions for creating a Docker container                 |
| Container       | A runnable instance of an image                                                        |
| Network         | Helps isolate container communications                                                 |
| Storage volumes | Help persist data                                                                      |
| Plugins         | Can provide additional capabilities, such as connections to external storage platforms |
| Add-ons         | Another Docker object mentioned in the lesson                                          |

## Dockerfile

A Dockerfile is a text file that contains the instructions needed to create an image.

You can create a Dockerfile using any editor from the console or terminal.

### Essential Dockerfile Instructions

A Dockerfile must always begin with a `FROM` instruction that defines a base image. Often, the base image is from a public repository, such as an operating system or a specific language like Go or Node.js.

| Instruction | Purpose                                 | Important detail                                                                                      |
| ----------- | --------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| `FROM`      | Defines a base image                    | A Dockerfile must always begin with `FROM`                                                            |
| `RUN`       | Executes commands                       | Used for command execution                                                                            |
| `CMD`       | Defines a default command for execution | A Dockerfile should have only one `CMD` instruction; if several exist, only the last one takes effect |

```dockerfile
FROM <base image>
RUN <command>
CMD <default command>
```

{% hint style="info" %}
The supplied lesson does not provide complete concrete values for these Dockerfile instructions.
{% endhint %}

## Docker Images

A Docker image is a read-only template with instructions for creating a Docker container.

The Dockerfile provides instructions to build the image, and each Docker instruction creates a new layer in the image.

```
Dockerfile
    │
    ├── FROM  → Layer
    ├── RUN   → Layer
    ├── CMD   → Layer / image configuration
    │
    ▼
Docker Image
```

### Rebuilding Images

When you change the Dockerfile and rebuild the image, the Docker engine only rebuilds the changed layers.

Images can share layers, which saves:

* Disk space.
* Network bandwidth when sending and receiving images.

| Event                         | Result described in the lesson       |
| ----------------------------- | ------------------------------------ |
| A Docker instruction is added | A new image layer is created         |
| The Dockerfile changes        | The image is rebuilt                 |
| A layer does not change       | It can be reused                     |
| A layer changes               | The Docker engine rebuilds it        |
| Multiple images share layers  | Disk space is saved                  |
| Images are transferred        | Shared layers save network bandwidth |

## From Image to Running Container

When you instantiate an image, you get a running container.

```
Docker Image
    ↓
Instantiate image
    ↓
Running Container
```

A writable container layer is placed on top of the read-only image layers. The writable layer is needed because containers are not immutable as images.

```
+-----------------------------------+
|     Writable Container Layer      |
+-----------------------------------+
|        Read-Only Image Layer      |
+-----------------------------------+
|        Read-Only Image Layer      |
+-----------------------------------+
|        Read-Only Image Layer      |
+-----------------------------------+
```

| Object    | Property described in the lesson |
| --------- | -------------------------------- |
| Image     | Read-only                        |
| Container | Has a writable container layer   |

## Container Image Naming

An image name has a unique format consisting of three parts:

1. Host name
2. Repository
3. Tag

```
<host-name>/<repository>:<tag>
```

| Component  | Meaning                                                              |
| ---------- | -------------------------------------------------------------------- |
| Host name  | Identifies the image registry                                        |
| Repository | A group of related container images                                  |
| Tag        | Provides information about a specific version or variant of an image |

### Example

```bash
docker.io/ubuntu:18.04
```

| Component  | Example     | Meaning                                 |
| ---------- | ----------- | --------------------------------------- |
| Host name  | `docker.io` | Refers to the Docker Hub registry       |
| Repository | `ubuntu`    | Indicates the Ubuntu image              |
| Tag        | `18.04`     | Represents the installed Ubuntu version |

When using the Docker CLI, you can exclude the `docker.io` host name:

```
ubuntu:18.04
```

## Docker Containers

A Docker container is a runnable instance of an image.

```
Docker Image
     ↓
Runnable instance
     ↓
Docker Container
```

You can use the Docker API or CLI to:

* Create.
* Start.
* Stop.
* Delete an image.

{% hint style="info" %}
The source uses the phrase “delete an image” in this container-management passage. That terminology is retained here.
{% endhint %}

You can also:

* Connect to multiple networks.
* Attach storage to the container.
* Create a new image based on its current state.

## Networks

Docker keeps containers well isolated from each other and their host machine.

Networks help isolate container communications.

```
Container A
     │
     ├── Network
     │
Container B
     │
     └── Network

Network isolation
        ↓
Container communication isolation
```

## Storage and Data Persistence

By default, data does not persist when the container no longer exists.

Docker uses volumes and bind mounts to persist data even after a container stops.

```
Container running
      ↓
Data exists
      ↓
Container stops / no longer exists
      ↓
Default container data does not persist

Persistence mechanisms:
      ├── Volumes
      └── Bind mounts
```

### Volumes

Volumes allow data to remain available even after a container stops.

```
Container
    │
    └── Volume
           ↓
      Persistent data
```

### Bind Mounts

Docker also uses bind mounts to persist data.

Volumes and bind mounts persist data even after a container stops.

## Storage Plugins

Docker supports plugins such as storage plugins.

Storage plugins provide the ability to connect to external storage platforms.

```
Docker Container
       ↓
Storage Plugin
       ↓
External Storage Platform
```

## Docker Object Lifecycle

```
Dockerfile
    ↓
Docker instructions
    ↓
Docker Image
    ↓
Image Layers
    ↓
Instantiate Image
    ↓
Running Container
    ↓
Networks + Storage
    ↓
External Storage through Plugins
```

```
Dockerfile
  │
  │ contains instructions
  ▼
Docker Image
  │
  │ read-only template
  │ consists of image layers
  ▼
Docker Container
  │
  │ runnable instance of image
  │ has writable container layer
  ├───────────────┐
  ▼               ▼
Networks        Storage
                  │
                  ▼
             Storage Plugins
                  │
                  ▼
        External Storage Platforms
```

## Lesson Summary

* Docker contains objects such as Dockerfiles, images, containers, networks, storage volumes, plugins, and add-ons.
* Essential Docker instructions include `FROM`, `RUN`, and `CMD`.
* A Docker container is a runnable instance of an image.
* An image name format consists of a host name, repository, and tag.
* Docker uses networks to isolate container communications.
* Docker uses volumes and bind mounts to persist data even after a container stops running.
* Plugins, such as storage plugins, provide the ability to connect to external storage platforms.

# Introduction to Containers

<figure><img src="../.gitbook/assets/Introduction to Containers Infographic1.png" alt=""><figcaption></figcaption></figure>

## Learning Objectives

After watching this video, you will be able to:

1. Identify the traditional computing issues for software development.
2. Define a container and describe its characteristics.
3. List container benefits and challenges.
4. List popular container vendors.

## Cloud-Native Development and Container Technology

Cloud-native is the newest application development approach for building scalable, dynamic, hybrid cloud-friendly software. Container technology is a powerful part of that approach.

## Shipping-Container Analogy

The modern shipping industry standardized a set of container sizes, so no matter what item is shipped, the container size remains the same. Standardization significantly improves shipping efficiency.

Logistics staff select container transport options based on the container’s size and the client’s delivery needs:

* Ships
* Planes
* Trains
* Trucks

Digital container technology is similar. Containers solve the problem of making software portable so that applications can run on multiple platforms.

## Definition of a Container

A container, powered by the containerization engine, is a standard unit of software that encapsulates the following items necessary for programmers to build, ship, and run applications efficiently:

* Application code
* Runtime
* System tools
* System libraries
* Settings

Operations and underlying infrastructure issues are no longer blockers.

Applications can be quickly moved between environments while maintaining confidence that the application will work correctly:

| From                | To                     |
| ------------------- | ---------------------- |
| Laptop              | Testing environment    |
| Staging environment | Production environment |
| Physical machine    | Virtual machine        |
| Private cloud       | Public cloud           |

A container can be small, just tens of megabytes, and developers can almost instantly start containerized applications.

With these capabilities, containers serve as the foundation for today’s development and deployment solutions standards.

## Traditional Computing Challenges

Organizations encounter development and deployment challenges with traditional computing environments.

### Application Isolation and Resource Allocation

In traditional environments, developers can’t isolate the app and allocate or designate specific storage and memory resources for apps on physical servers.

### Poor Server Utilization

Servers are often underutilized or overutilized, leading to poor utilization and a poor return on investment.

### Provisioning and Maintenance

Traditional deployments require comprehensive provisioning resources and expensive maintenance costs.

### Peak Workload Performance

The limits of physical servers can constrain application performance during peak workloads.

### Portability Limitations

Applications are not portable across multiple environments and operating systems.

### Resiliency

Implementing hardware for resiliency is often time-consuming, complex, and expensive.

### Scalability

Traditional on-premises IT environments have limited scalability.

### Automation

Automation is challenging when distributing software to multiple platforms and resources using traditional environments.

## How Containers Address Traditional Challenges

Containers enable organizations to overcome these challenges.

### Container Engines

Container engines virtualize the operating system and are responsible for running containers.

### Container Characteristics

Platform-independent containers are:

* Lightweight
* Fast
* Isolated
* Portable
* Secure
* Often require less memory space

Binaries, libraries, and other entities within the container enable applications to run. One machine can host multiple containers.

### Deployment and Independence

Containers help programmers quickly deploy code into applications.

Containers are platform-independent and can run on:

* The cloud
* The desktop
* On-premises environments

Containers, being operating-system-independent, run on:

* Windows
* Linux
* Mac OS

Containers are also programming-language and IDE independent, whether you are running:

* Python
* Node
* Java
* Other languages

## Container Benefits for Organizations

Containers enable organizations to:

1. Quickly create applications using automation.
2. Lower deployment time and costs.
3. Improve resource utilization, including CPU and memory.
4. Port across different environments.
5. Support next-gen applications, including microservices.

| Benefit                      | Source detail                                          |
| ---------------------------- | ------------------------------------------------------ |
| Application creation         | Quickly create applications using automation           |
| Deployment                   | Lower deployment time and costs                        |
| Resource utilization         | Improve utilization, including CPU and memory          |
| Portability                  | Port across different environments                     |
| Next-generation applications | Support next-gen applications, including microservices |

## Containerization Challenges

Using containerization is not without its challenges.

| Challenge              | Source detail                                                                       |
| ---------------------- | ----------------------------------------------------------------------------------- |
| Server security        | Security can become an issue if the server’s operating system is affected           |
| Large-scale management | Developers can become overwhelmed when managing thousands of containers             |
| Legacy migration       | Converting monolithic legacy applications can be a complex process                  |
| Right-sizing           | Developers can experience difficulty right-sizing containers for specific scenarios |

## Popular Container Vendors

| Vendor / technology | Description from the source                                               |
| ------------------- | ------------------------------------------------------------------------- |
| **Docker**          | A robust platform and the most popular container platform today           |
| **Podman**          | A daemon-less container engine that is more secure than Docker            |
| **LXC**             | Developers often prefer it for data-intensive applications and operations |
| **Vagrant**         | Offers the highest levels of isolation on the running physical machine    |

> The descriptions in this section are preserved from the supplied lesson and are not independently evaluated or corrected.

## Overall Relationship Between Traditional Computing Problems and Containers

Organizations are moving to containers to overcome challenges around:

* Isolation
* Utilization
* Provisioning
* Performance
* And more

Containers provide a standard software unit that packages what is needed to build, ship, and run applications while improving portability and addressing several traditional infrastructure limitations.

## Container Characteristics Reference

| Characteristic                   | Source meaning                                                                |
| -------------------------------- | ----------------------------------------------------------------------------- |
| Standard unit of software        | A container encapsulates what is needed to build, ship, and run applications  |
| Portable                         | Applications can run across multiple platforms and environments               |
| Lightweight                      | Containers can be as small as tens of megabytes                               |
| Fast                             | Containerized applications can almost instantly start                         |
| Isolated                         | Containers provide application/process isolation                              |
| Secure                           | The source identifies security as a container characteristic                  |
| Platform-independent             | Containers can run on cloud, desktop, and on-premises environments            |
| Operating-system-independent     | Containers can run on Windows, Linux, and Mac OS                              |
| Programming-language-independent | The source gives Python, Node, and Java as examples                           |
| IDE-independent                  | The source explicitly describes containers as IDE independent                 |
| Resource efficient               | Containers often require less memory space and improve CPU/memory utilization |
| Multi-container capable          | One machine can host multiple containers                                      |

## Traditional Environment vs. Container-Based Approach

| Traditional environment issue                              | Container-related capability described by the source               |
| ---------------------------------------------------------- | ------------------------------------------------------------------ |
| Applications cannot be easily isolated on physical servers | Containers provide isolation                                       |
| Difficult resource allocation/designation                  | Containers improve resource utilization, including CPU and memory  |
| Underutilized or overutilized servers                      | Containers improve utilization                                     |
| Poor return on investment                                  | Lower deployment time and costs and improved utilization           |
| Extensive provisioning requirements                        | Containers support automation and easier deployment                |
| Expensive maintenance                                      | Containers lower deployment time and costs                         |
| Peak workload performance constraints                      | Containers address performance and resource-management limitations |
| Poor portability across environments and operating systems | Containers are portable and platform-independent                   |
| Expensive and complex physical resiliency                  | Container-based approaches address infrastructure limitations      |
| Limited on-premises scalability                            | Containers support scaling and multiple containers per machine     |
| Difficult automation across platforms and resources        | Containers enable automation                                       |

## Deployment and Portability Examples

Applications can be moved while maintaining confidence that they will work correctly:

```
Laptop
  → Testing environment

Staging environment
  → Production environment

Physical machine
  → Virtual machine

Private cloud
  → Public cloud
```

## Resource and Infrastructure Concepts Mentioned

* Storage
* Memory
* CPU
* Physical servers
* Physical machines
* Virtual machines
* Private cloud
* Public cloud
* Desktop
* On-premises infrastructure
* Operating systems
* Binaries
* Libraries
* System tools
* System libraries
* Runtime
* Application code
* Settings

## Development and Application Technologies Mentioned

| Technology / concept    | Context in the lesson                              |
| ----------------------- | -------------------------------------------------- |
| Cloud-native            | Application development approach                   |
| Containers              | Portable units of software                         |
| Containerization engine | Powers a container                                 |
| Container engines       | Virtualize the operating system and run containers |
| Microservices           | Example of a next-generation application           |
| Python                  | Example programming language                       |
| Node                    | Example programming language/runtime               |
| Java                    | Example programming language                       |
| IDEs                    | Containers are described as IDE-independent        |

## Final Lesson Summary

* Organizations are moving to containers to overcome challenges around isolation, utilization, provisioning, performance, and more.
* A container is a standard unit of software that encapsulates everything needed to build, ship, and run applications.
* Containers are operating-system-independent.
* Containers are programming-language-independent.
* Containers are platform-independent.
* Containers lower deployment time and costs.
* Containers improve utilization.
* Containers automate processes.
* Containers support next-generation applications, including microservices.
* Developers may find management, legacy project migration, and right-sizing to be significant challenges.
* Major container vendors include Docker, Podman, LXC, and Vagrant.

## Commands and Code

The supplied lesson does not contain executable commands, command-line examples, code snippets, YAML, JSON, Dockerfiles, or configuration examples.

The source mentions product and platform names such as **Docker**, **Podman**, **LXC**, and **Vagrant**, but these are technologies and vendors in this lesson, not command examples.

<details>

<summary>Complete Source Transcript</summary>

Welcome to “Introduction to Containers.” After watching this video, you will be able to identify the traditional computing issues for software development, define a container and describe its characteristics, and list container benefits and challenges, and popular container vendors. Cloud-native is the newest application development approach for building scalable, dynamic, hybrid cloud-friendly software. And container technology is a powerful part of that approach. Let’s check out the analogy of a shipping container. The modern shipping industry standardized a set of container sizes, so no matter what item is shipped, the container size remains the same. Standardization significantly improves shipping efficiency. Logistics staff select container transport options such as ships, planes, trains, and trucks, based on the container’s size and the client’s delivery needs. Digital container technology is similar. Containers solve the problem of making software portable so that applications can run on multiple platforms. A container, powered by the containerization engine, is a standard unit of software that encapsulates the application code, runtime, system tools, system libraries, and settings necessary for programmers to build, ship, and run applications efficiently. Operations and underlying infrastructure issues are no longer blockers. You can quickly move applications from your laptop to a testing environment, from a staging environment to a production environment, from a physical machine to a virtual machine, or a private cloud or public cloud, and always know that your application will work correctly. A container can be small, just tens of megabytes, and developers can almost instantly start containerized applications. With these capabilities, containers serve as the foundation for today’s development and deployment solutions standards. Let’s examine some of the development and deployment challenges organizations encounter with traditional computing environments. In traditional environments, developers can’t isolate the app and allocate or designate specific storage and memory resources for apps on physical servers. Servers are often underutilized or overutilized, leading to poor utilization and a poor return on investment. Traditional deployments require comprehensive provisioning resources and expensive maintenance costs. The limits of physical servers can constrain application performance during peak workloads. Applications are not portable across multiple environments and operating systems. Implementing hardware for resiliency is often time-consuming, complex and expensive. Traditional on premises IT environments have limited scalability, and Finally, automation is challenging when distributing software to multiple platforms and resources using traditional environments. Containers enable organizations to overcome these challenges. Container engines virtualize the operating system and are responsible for running containers. Platform-independent containers are lightweight, fast, isolated, portable, and secure and often require less memory space. Binaries, libraries, and other entities within the container enable apps to run, and one machine can host multiple containers. Containers help programmers quickly deploy code into applications Containers are platform-independent and can run on the cloud, desktop, and on-premises Containers being operating system-independent, run on Windows, Linux, or Mac OS. Containers are also programming language and IDE independent—whether you are running Python, Node, Java, or other languages. Containers enable organizations to: Quickly create applications using automation. Lower deployment time and costs. Improve resource utilization, including CPU and memory. Port across different environments, and support next-gen applications, including microservices. Using containerization is not without its challenges. Server security can become an issue if its operating system is affected. Developers can become overwhelmed when managing thousands of containers. Converting monolithic legacy applications can be a complex process, and Developers can experience difficulty right-sizing containers for specific scenarios. Next, let’s learn about some of the more popular container vendors. Docker is a robust platform and the most popular container platform today. Podman is a daemon-less container engine that is more secure than Docker. Developers often prefer LXC for data-intensive applications and operations. And, Vagrant offers the highest levels of isolation on the running physical machine. In this video, you learned that organizations are moving to containers to overcome challenges around isolation, utilization, provisioning, performance, and more. A container is a standard unit of software that encapsulates everything needed to build, ship, and run applications. Containers are operating system, programming language, and platform-independent. They lower deployment time and costs, improve utilization, automate processes, and support next-gen applications (microservices). Developers may find that management, legacy project migration, and right-sizing are significant challenges. And finally, major container vendors include Docker, Podman, LXC, and Vagrant.

</details>

<details>

<summary>Complete VTT Cue Transcript</summary>

| Cue | Timestamp                       | Subtitle text                                                                                             |
| --: | ------------------------------- | --------------------------------------------------------------------------------------------------------- |
|   1 | `00:00:08.080 --> 00:00:11.180` | Welcome to “Introduction to Containers.”                                                                  |
|   2 | `00:00:11.180 --> 00:00:14.260` | After watching this video, you will be able to                                                            |
|   3 | `00:00:14.260 --> 00:00:18.201` | identify the traditional computing issues for software development,                                       |
|   4 | `00:00:18.201 --> 00:00:21.748` | define a container and describe its characteristics, and                                                  |
|   5 | `00:00:21.748 --> 00:00:27.258` | list container benefits and challenges, and popular container vendors.                                    |
|   6 | `00:00:27.258 --> 00:00:33.050` | Cloud-native is the newest application development approach for building scalable, dynamic, hybrid        |
|   7 | `00:00:33.050 --> 00:00:34.796` | cloud-friendly software.                                                                                  |
|   8 | `00:00:34.796 --> 00:00:38.680` | And container technology is a powerful part of that approach.                                             |
|   9 | `00:00:39.110 --> 00:00:42.650` | Let’s check out the analogy of a shipping container.                                                      |
|  10 | `00:00:42.650 --> 00:00:46.430` | The modern shipping industry standardized a set of container sizes,                                       |
|  11 | `00:00:46.430 --> 00:00:51.000` | so no matter what item is shipped, the container size remains the same.                                   |
|  12 | `00:00:51.000 --> 00:00:55.660` | Standardization significantly improves shipping efficiency.                                               |
|  13 | `00:00:55.660 --> 00:01:01.580` | Logistics staff select container transport options such as ships, planes, trains, and                     |
|  14 | `00:01:01.580 --> 00:01:06.300` | trucks, based on the container’s size and the client’s delivery needs.                                    |
|  15 | `00:01:06.300 --> 00:01:09.030` | Digital container technology is similar.                                                                  |
|  16 | `00:01:09.030 --> 00:01:14.890` | Containers solve the problem of making software portable so that applications can run on multiple         |
|  17 | `00:01:14.890 --> 00:01:16.029` | platforms.                                                                                                |
|  18 | `00:01:16.599 --> 00:01:21.800` | A container, powered by the containerization engine, is a standard unit of software that                  |
|  19 | `00:01:21.800 --> 00:01:26.250` | encapsulates the application code, runtime, system tools,                                                 |
|  20 | `00:01:26.250 --> 00:01:32.140` | system libraries, and settings necessary for programmers to build, ship, and run applications             |
|  21 | `00:01:32.140 --> 00:01:33.354` | efficiently.                                                                                              |
|  22 | `00:01:33.354 --> 00:01:39.620` | Operations and underlying infrastructure issues are no longer blockers. You can quickly move              |
|  23 | `00:01:39.620 --> 00:01:40.620` | applications                                                                                              |
|  24 | `00:01:40.620 --> 00:01:43.340` | from your laptop to a testing environment,                                                                |
|  25 | `00:01:43.340 --> 00:01:46.690` | from a staging environment to a production environment,                                                   |
|  26 | `00:01:46.690 --> 00:01:52.020` | from a physical machine to a virtual machine, or a private cloud or public cloud,                         |
|  27 | `00:01:52.020 --> 00:01:55.842` | and always know that your application will work correctly.                                                |
|  28 | `00:01:55.842 --> 00:02:02.877` | A container can be small, just tens of megabytes, and developers can almost instantly start containerized |
|  29 | `00:02:02.877 --> 00:02:03.877` | applications.                                                                                             |
|  30 | `00:02:03.877 --> 00:02:08.459` | With these capabilities, containers serve as the foundation for today’s development                       |
|  31 | `00:02:08.459 --> 00:02:11.110` | and deployment solutions standards.                                                                       |
|  32 | `00:02:11.110 --> 00:02:16.340` | Let’s examine some of the development and deployment challenges organizations encounter                   |
|  33 | `00:02:16.340 --> 00:02:19.480` | with traditional computing environments.                                                                  |
|  34 | `00:02:19.480 --> 00:02:24.620` | In traditional environments, developers can’t isolate the app and allocate or designate                   |
|  35 | `00:02:24.620 --> 00:02:30.060` | specific storage and memory resources for apps on physical servers.                                       |
|  36 | `00:02:30.060 --> 00:02:35.980` | Servers are often underutilized or overutilized, leading to poor utilization and a poor return            |
|  37 | `00:02:35.980 --> 00:02:37.238` | on investment.                                                                                            |
|  38 | `00:02:37.238 --> 00:02:43.260` | Traditional deployments require comprehensive provisioning resources and expensive maintenance            |
|  39 | `00:02:43.260 --> 00:02:44.360` | costs.                                                                                                    |
|  40 | `00:02:44.360 --> 00:02:49.692` | The limits of physical servers can constrain application performance during peak workloads.               |
|  41 | `00:02:49.907 --> 00:02:55.116` | Applications are not portable across multiple environments and operating systems.                         |
|  42 | `00:02:55.331 --> 00:03:01.657` | Implementing hardware for resiliency is often time-consuming, complex and expensive.                      |
|  43 | `00:03:01.657 --> 00:03:05.690` | Traditional on premises IT environments have limited scalability, and                                     |
|  44 | `00:03:05.690 --> 00:03:12.560` | Finally, automation is challenging when distributing software to multiple platforms and resources         |
|  45 | `00:03:12.560 --> 00:03:15.157` | using traditional environments.                                                                           |
|  46 | `00:03:15.157 --> 00:03:20.127` | Containers enable organizations to overcome these challenges.                                             |
|  47 | `00:03:20.190 --> 00:03:26.371` | Container engines virtualize the operating system and are responsible for running containers.             |
|  48 | `00:03:26.371 --> 00:03:32.590` | Platform-independent containers are lightweight, fast, isolated, portable, and secure and often           |
|  49 | `00:03:32.590 --> 00:03:34.360` | require less memory space.                                                                                |
|  50 | `00:03:34.360 --> 00:03:40.550` | Binaries, libraries, and other entities within the container enable apps to run, and one                  |
|  51 | `00:03:40.550 --> 00:03:43.365` | machine can host multiple containers.                                                                     |
|  52 | `00:03:43.365 --> 00:03:48.126` | Containers help programmers quickly deploy code into applications                                         |
|  53 | `00:03:48.126 --> 00:03:54.286` | Containers are platform-independent and can run on the cloud, desktop, and on-premises                    |
|  54 | `00:03:54.286 --> 00:04:00.411` | Containers being operating system-independent, run on Windows, Linux, or Mac OS.                          |
|  55 | `00:04:00.411 --> 00:04:05.720` | Containers are also programming language and IDE independent—whether you are running                      |
|  56 | `00:04:05.720 --> 00:04:09.451` | Python, Node, Java, or other languages.                                                                   |
|  57 | `00:04:09.552 --> 00:04:12.170` | Containers enable organizations to:                                                                       |
|  58 | `00:04:12.170 --> 00:04:15.300` | Quickly create applications using automation.                                                             |
|  59 | `00:04:15.300 --> 00:04:17.546` | Lower deployment time and costs.                                                                          |
|  60 | `00:04:17.546 --> 00:04:22.410` | Improve resource utilization, including CPU and memory.                                                   |
|  61 | `00:04:22.410 --> 00:04:24.380` | Port across different environments,                                                                       |
|  62 | `00:04:24.380 --> 00:04:28.953` | and support next-gen applications, including microservices.                                               |
|  63 | `00:04:29.118 --> 00:04:33.403` | Using containerization is not without its challenges.                                                     |
|  64 | `00:04:33.403 --> 00:04:38.595` | Server security can become an issue if its operating system is affected.                                  |
|  65 | `00:04:38.595 --> 00:04:43.199` | Developers can become overwhelmed when managing thousands of containers.                                  |
|  66 | `00:04:43.199 --> 00:04:48.427` | Converting monolithic legacy applications can be a complex process, and                                   |
|  67 | `00:04:48.427 --> 00:04:54.162` | Developers can experience difficulty right-sizing containers for specific scenarios.                      |
|  68 | `00:04:54.162 --> 00:04:58.879` | Next, let’s learn about some of the more popular container vendors.                                       |
|  69 | `00:04:58.879 --> 00:05:03.819` | Docker is a robust platform and the most popular container platform today.                                |
|  70 | `00:05:03.819 --> 00:05:08.705` | Podman is a daemon-less container engine that is more secure than Docker.                                 |
|  71 | `00:05:08.705 --> 00:05:13.879` | Developers often prefer LXC for data-intensive applications and operations.                               |
|  72 | `00:05:13.879 --> 00:05:20.839` | And, Vagrant offers the highest levels of isolation on the running physical machine.                      |
|  73 | `00:05:20.839 --> 00:05:22.839` | In this video, you learned that                                                                           |
|  74 | `00:05:22.839 --> 00:05:28.719` | organizations are moving to containers to overcome challenges around isolation, utilization,              |
|  75 | `00:05:28.719 --> 00:05:31.469` | provisioning, performance, and more.                                                                      |
|  76 | `00:05:31.469 --> 00:05:36.729` | A container is a standard unit of software that encapsulates everything needed to build,                  |
|  77 | `00:05:36.729 --> 00:05:39.029` | ship, and run applications.                                                                               |
|  78 | `00:05:39.029 --> 00:05:44.349` | Containers are operating system, programming language, and platform-independent.                          |
|  79 | `00:05:44.349 --> 00:05:50.520` | They lower deployment time and costs, improve utilization, automate processes, and support                |
|  80 | `00:05:50.520 --> 00:05:53.714` | next-gen applications (microservices).                                                                    |
|  81 | `00:05:53.892 --> 00:05:59.944` | Developers may find that management, legacy project migration, and right-sizing are significant           |
|  82 | `00:05:59.944 --> 00:06:00.944` | challenges.                                                                                               |
|  83 | `00:06:01.349 --> 00:06:07.938` | And finally, major container vendors include Docker, Podman, LXC, and Vagrant.                            |

</details>

<details>

<summary>Source Reconciliation</summary>

## TXT and VTT Comparison

The TXT transcript and VTT subtitle transcript contain the same spoken content.

The comparison was performed after normalizing whitespace:

* TXT normalized transcript length: 5,269 characters.
* VTT normalized transcript length: 5,269 characters.
* Normalized transcript comparison: **match**.

The TXT is therefore used as the complete continuous transcript, while the VTT is preserved separately as a timestamped cue index.

## Terminology Fidelity

The source contains phrases and descriptions such as:

* “Cloud-native is the newest application development approach”
* “Podman is a daemon-less container engine that is more secure than Docker”
* “Vagrant offers the highest levels of isolation on the running physical machine”

These statements are preserved as source-derived statements. They have not been independently corrected, ranked, or replaced with external technical claims.

## Completeness

This document preserves:

* Learning objectives.
* Cloud-native context.
* Shipping-container analogy.
* Container definition.
* Containerized components.
* Portability examples.
* Traditional computing challenges.
* Container-engine role.
* Container characteristics.
* Platform, operating-system, programming-language, and IDE independence.
* Organizational benefits.
* Containerization challenges.
* Vendor descriptions.
* Final lesson conclusions.
* The complete original TXT transcript.
* All VTT subtitle cues and timestamps.

</details>

# Builds

<figure><img src="../.gitbook/assets/OpenShift Builds Infographic.png" alt=""><figcaption></figcaption></figure>

## Overview

This document captures the complete content of the supplied `Builds.txt`, `Builds-subtitles-en.vtt`, and `Builds.mp4` sources, merged into a single technical reference. The lesson explains what a build is, build configuration and input sources, ImageStreams, build triggers, BuildConfig processing, Source-to-Image (S2I), Docker and custom build strategies, and CI/CD build automation. The MP4 was also inspected for slide-level visual content and the relevant visuals are referenced below.

## Table of Contents

* [Source Coverage and Reconciliation](builds.md#source-coverage-and-reconciliation)
* [Learning Objectives](builds.md#learning-objectives)
* [What Is a Build](builds.md#what-is-a-build)
* [Build Configuration](builds.md#build-configuration)
* [Build Input Sources](builds.md#build-input-sources)
* [ImageStreams](builds.md#imagestreams)
* [Build Triggers](builds.md#build-triggers)
* [BuildConfig Step-by-Step Process](builds.md#buildconfig-step-by-step-process)
* [Source-to-Image (S2I) Strategy](builds.md#source-to-image-s2i-strategy)
* [Docker Build Strategy](builds.md#docker-build-strategy)
* [Custom Build Strategy](builds.md#custom-build-strategy)
* [Build Automation and CI/CD](builds.md#build-automation-and-cicd)
* [End-to-End Build Flow](builds.md#end-to-end-build-flow)
* [Video Visual Context](builds.md#video-visual-context)
* [Key Terms / Glossary](builds.md#key-terms--glossary)
* [Command Reference](builds.md#command-reference)
* [Source Notes](builds.md#source-notes)
* [Complete Cleaned Transcript](builds.md#complete-cleaned-transcript)
* [VTT Timing Index](builds.md#vtt-timing-index)

## Source Coverage and Reconciliation

| Source                        | Result                             |
| ----------------------------- | ---------------------------------- |
| `Builds.txt`                  | Complete written transcript        |
| `Builds-subtitles-en.vtt`     | Timestamped transcript             |
| `Builds.mp4`                  | Original video; visually inspected |
| TXT line count                | **84**                             |
| VTT cue count                 | **102**                            |
| TXT/VTT normalized transcript | **Exact match**                    |
| Video duration                | **445.3 seconds (\~7:25)**         |
| Video format                  | H.264 video + AAC audio            |
| Video resolution              | 428 × 240                          |

The TXT and VTT contain the same spoken material after whitespace normalization. The VTT is therefore used in this document primarily for timing/navigation, while the spoken content is represented once in structured form.

## Learning Objectives

The video states that, after watching it, you will be able to:

1. Describe what a build is.
2. Describe build input sources and build strategy.
3. Describe what ImageStreams do and identify their features.
4. Explain how to automate builds using build triggers.
5. List the steps used for the BuildConfig process.
6. Explain Source-to-Image, Docker, and custom build strategies.

The introductory visual slide groups these learning goals around:

* Builds, input sources, and build strategy.
* ImageStreams and their features.
* Build triggers.
* BuildConfig process.
* Source-to-Image, Docker, and custom build strategies.

## What Is a Build

A **build** is the process of transforming inputs into a resultant object.

The example given is:

```
Source code → Container image
```

The source defines a build as transforming source code into a container image.

A build requires a **BuildConfig**, which is a build configuration file.

The BuildConfig defines:

* The build strategy.
* The build input sources.

## Build Configuration

A build requires a build configuration file, also called a **BuildConfig**.

The BuildConfig determines:

| BuildConfig responsibility | Source meaning                                |
| -------------------------- | --------------------------------------------- |
| Build strategy             | Defines how the build is executed             |
| Input sources              | Defines what content is supplied to the build |

The lesson later demonstrates a sample BuildConfig called `ruby-sample-build`.

## Build Input Sources

A build input source provides content for builds.

The source lists the build inputs in order of precedence:

| Precedence | Build input source                     |
| ---------: | -------------------------------------- |
|          1 | Inline Dockerfile definitions          |
|          2 | Content extracted from existing images |
|          3 | Git repositories                       |
|          4 | Binary or local inputs                 |
|          5 | Input secrets                          |
|          6 | External artifacts                     |

### Multiple Inputs

Multiple inputs can be combined into a single build.

### Inline Dockerfile Precedence

An inline Dockerfile takes precedence over an external Dockerfile.

The source states that the inline Dockerfile:

* Takes precedence.
* Overwrites the external Dockerfile.

> **Note:** The transcript uses the wording “overwrites any external Dockerfile.” That wording is preserved as source content.

## ImageStreams

An **ImageStream** is an abstraction for referencing container images within OpenShift.

### What an ImageStream Does

The source states that an ImageStream:

* Continuously creates and updates container images.
* Does **not** contain actual image data.
* Instead, points to images stored in internal registries, external registries, or other ImageStreams.

Conceptually:

```
ImageStream
    ↓
References image
    ↓
Internal Registry / External Registry / Other ImageStream
```

### Tags

A single ImageStream can contain many different tags.

Examples given:

```
latest
dev
test
```

Each tag points to a particular image in a registry.

### Deployment Through ImageStreamTags

For application deployment, the source recommends referring to the **ImageStream tag** instead of hardcoding:

* Registry URL.
* Image tag.

If the source image location changes, you update the ImageStream definition instead of individually updating every deployment.

This creates a decoupling relationship:

```
Deployment
    ↓
ImageStreamTag
    ↓
Actual registry image
```

### ImageStream Trigger Capability

An ImageStream also provides a trigger capability.

When a new image version becomes available, it can automatically invoke:

* Builds.
* Deployments.

## Build Triggers

Instead of running builds manually, the source recommends automating builds using triggers.

The lesson presents three trigger types.

### 1. Webhook Trigger

A webhook trigger:

* Sends a request to an API endpoint.

It supports:

* Generic webhooks.
* GitHub webhooks.

GitHub webhooks are described as commonly used.

They can send trigger requests on:

* A new commit.
* A pull request.
* Other circumstances.

### 2. Image Change Trigger

An image change trigger starts a build when a new version of an image becomes available.

The source gives this example:

* An application is built using a Node.js base image.
* The base image is updated when security fixes are released and other updates occur.
* The new version can therefore trigger a build.

### 3. Configuration Change Trigger

A configuration change trigger causes a new build to run when a new BuildConfig resource is created.

### Trigger Summary

| Trigger              | Event                                          | Result                                   |
| -------------------- | ---------------------------------------------- | ---------------------------------------- |
| Webhook              | API request such as GitHub commit/pull request | Trigger request reaches the API endpoint |
| Image change         | New image version                              | Build is triggered                       |
| Configuration change | New BuildConfig resource                       | New build runs                           |

## BuildConfig Step-by-Step Process

The lesson shows a sample configuration file for a BuildConfig.

The specification creates a new BuildConfig named:

```
ruby-sample-build
```

### Run Policy

The `runPolicy` field controls how builds created from a BuildConfig run.

The source names these values:

```
default
serial
sequentially
simultaneously
```

> ⚠️ **Unclear in source:** The wording describing the `runPolicy` values is presented exactly as spoken. The visual example specifically shows `runPolicy: "Serial"`.

### Triggers

The BuildConfig can specify a list of triggers that creates a new build.

### Source Section

The `source` section defines the build source.

The source type determines the primary input.

Examples include:

* Git repository.
* Inline Dockerfile.
* Binary payloads.

### Strategy Section

The `strategy` section specifies the strategy used to execute the build.

The source names:

* Source-to-Image.
* Docker.
* Custom.

The sample uses:

* The `ruby-20-centos7` container image.
* The Source-to-Image (S2I) strategy.

### Output Section

After building the container image:

* The image is pushed into the repository described in the `output` section.

### `postCommit`

The `postCommit` section defines an optional build hook.

The video visibly shows a hook script associated with the sample BuildConfig:

```yaml
postCommit:
  script: "bundle exec rake test"
```

> **Source visual note:** The exact YAML sample is shown in the video and is therefore preserved here as visible video content. The frame is low-resolution; only the fields that can be read confidently are reproduced as code.

### Visual BuildConfig Example

The video shows a YAML-like BuildConfig containing these visible elements:

```yaml
apiVersion: build.openshift.io/v1
kind: BuildConfig
metadata:
  name: "ruby-sample-build"
spec:
  runPolicy: "Serial"
  triggers:
    - type: "GitHub"
      secret: "secret101"
    - type: "Generic"
      secret: "secret101"
    - type: "ImageChange"
  source:
    git:
      uri: "https://github.com/openshift/ruby-hello-world"
  strategy:
    sourceStrategy:
      from:
        kind: "ImageStreamTag"
        name: "ruby-20-centos7:latest"
  output:
    to:
      kind: "ImageStreamTag"
      name: "origin-ruby-sample:latest"
  postCommit:
    script: "bundle exec rake test"
```

> ⚠️ **Unclear in source/video:** The low-resolution frame makes some YAML punctuation/formatting difficult to verify visually. The structure and values above are based on the visible slide; consult the original video frame for the exact presentation.

### BuildConfig Process — Step Summary

The visual “BuildConfig: Step-by-step process” slide shows:

1. Create a new BuildConfig called `ruby-sample-build`.
2. `runPolicy` controls how builds run; the example uses `Serial`.
3. Triggers define events that create a new build.
4. The `source` section defines build input source and strategy.
5. The input source type is Git with a URI.
6. The source strategy is S2I using `ruby-20-centos7`.
7. The output section specifies the container image repository; an optional `postCommit` hook can run tests.

## Source-to-Image (S2I) Strategy

**Source-to-Image**, or **S2I**, is another build strategy offered by OpenShift.

The source states that S2I:

* Builds reproducible container images.
* Injects application source into a builder image.
* Produces a ready-to-run image.
* Avoids using a Dockerfile.

### S2I Build Model

The source describes the new image as being built by incorporating:

* A builder image.
* The application source.

This enables going from source to image in a single step.

Conceptually:

```
Builder Image + Application Source
              ↓
             S2I
              ↓
       Ready-to-run Image
```

### Builder Images

OpenShift comes with a variety of available builder images.

This saves:

* Time.
* Development effort.

The video’s S2I diagram visually shows:

```
Code → S2I Build → Builder Image → Container Image → Nodes
```

It also shows developer configuration of deployment strategies and operations configuration of deployment strategies around the build/deploy flow.

## Docker Build Strategy

The Docker build strategy requires a repository that contains:

* A Dockerfile.
* Necessary artifacts.

When a build is started:

1. OpenShift takes the input.
2. OpenShift invokes the Docker build command.
3. The image is created.
4. The image is pushed to the internal OpenShift registry.

### Command Mentioned in the Source

```bash
docker build
```

The source does not provide flags or complete argument syntax.

### Four Ways to Implement the Docker Build Strategy

The lesson names four approaches:

1. Replace Dockerfile from image.
2. Use Dockerfile path.
3. Use Docker environment variables.
4. Add Docker build arguments.

These are displayed together on the Docker build strategy slide.

### Docker Build Strategy Summary

| Element      | Source detail                                |
| ------------ | -------------------------------------------- |
| Repository   | Must contain Dockerfile + required artifacts |
| Build action | OpenShift invokes the Docker build command   |
| Result       | Container image                              |
| Destination  | Internal OpenShift registry                  |
| Method 1     | Replace Dockerfile from image                |
| Method 2     | Use Dockerfile path                          |
| Method 3     | Use Docker environment variables             |
| Method 4     | Add Docker build arguments                   |

## Custom Build Strategy

In a **custom build strategy**, you must define and create your own builder image.

### Custom Builder Image

Custom builder images are regular Docker images that contain the logic required to:

```
Inputs
  ↓
Custom Builder Image
  ↓
Expected Outputs
```

### Additional Outputs

The source states that custom build strategies can create additional objects, including:

* JAR files.
* CI/CD deployment that performs unit tests.
* CI/CD deployment that performs integration tests.

### Availability

Custom builds are only available to:

* Cluster administrators.

The source states the reason:

* Custom builds run with high privileges.

### Comparison with Docker and S2I

Both Docker and S2I strategies result in runnable images.

The custom build strategy can additionally create objects such as JAR files and CI/CD deployment that performs testing.

## Build Automation and CI/CD

Cloud-native development requires greater automation throughout the container lifecycle.

The source identifies **Continuous Integration and Continuous Delivery (CI/CD)** as the mechanism for this automation.

### OpenShift CI/CD Process

The source describes the OpenShift CI/CD process as:

1. Automatically merge new code requests to the repository.
2. Build a new version.
3. Test the new version.
4. Approve the new version.
5. Deploy the new version to different environments.

Conceptually:

```
Code request
     ↓
Merge to repository
     ↓
Build
     ↓
Test
     ↓
Approve
     ↓
Deploy
     ↓
Different environments
```

The video visually represents this as a sequence of automated stages.

## End-to-End Build Flow

The complete source-supported process can be represented as:

```
Build Inputs
    ↓
BuildConfig
    ↓
Build Strategy
    ├── S2I
    ├── Docker
    └── Custom
    ↓
Build Execution
    ↓
Container Image / Resultant Object
    ↓
Output Repository / ImageStream
    ↓
Deployment
```

Automation can be added through:

```
Webhook Trigger
Image Change Trigger
Configuration Change Trigger
```

And CI/CD extends this into:

```
Merge
  ↓
Build
  ↓
Test
  ↓
Approve
  ↓
Deploy
```

## Video Visual Context

The MP4 was inspected for slide-level information that complements the transcript.

### Learning Objectives Slide

_Source: video, \~00:40. The slide visually groups the lesson objectives around builds/input sources, ImageStreams, triggers, BuildConfig, and build strategies._

### What Is a Build

_Source: video, \~00:45. The slide defines a build as transforming inputs into a resultant object and notes that BuildConfig defines the build strategy and input sources._

### Build Input Sources

_Source: video, \~01:20. The slide displays the six input sources in precedence order and notes that multiple inputs can be combined._

### ImageStream

_Source: video, \~02:20. The slide shows `latest`, `dev`, and `test` tags pointing to images in registries and summarizes ImageStream abstraction and trigger behavior._

### Build Triggers

_Source: video, \~02:40. The slide introduces webhook triggers and later reveals image-change and configuration-change triggers._

### BuildConfig — Steps 1–3

_Source: video, \~03:40. The slide begins the sample BuildConfig workflow with the `ruby-sample-build` name, run policy, and trigger list._

### BuildConfig — Steps 4–7

_Source: video, \~04:15. The slide shows source, Git input, S2I strategy, `ruby-20-centos7`, output image, and optional post-commit hook._

### Source-to-Image Strategy

_Source: video, \~04:45. The diagram shows source and builder-image flow into a container image, with deployment-related configuration around the process._

### Docker Build Strategy

_Source: video, \~05:25. The slide explains the Docker Registry flow and the four Docker build-strategy implementation methods._

### Custom Build Strategy

_Source: video, \~05:55. The slide describes custom builder images, additional outputs, and the administrative restriction._

### Builds Automation

_Source: video, \~06:30. The slide introduces CI/CD automation; later frames show the process progressing from repository merge through build/test and deployment._

### Recap

_Source: video, \~07:00. The final recap slide restates the definition of a build, input precedence, ImageStreams, triggers, common strategies, and the BuildConfig requirement._

## Key Terms / Glossary

| Term                             | Definition / meaning from the source                                                           |
| -------------------------------- | ---------------------------------------------------------------------------------------------- |
| **Build**                        | Process of transforming inputs into a resultant object                                         |
| **BuildConfig**                  | Build configuration file defining build strategy and input sources                             |
| **Build strategy**               | Method used to execute a build                                                                 |
| **Build input source**           | Content provided as input to a build                                                           |
| **ImageStream**                  | OpenShift abstraction for referencing container images                                         |
| **ImageStream tag**              | Tag within an ImageStream pointing to a particular image                                       |
| **Webhook trigger**              | Trigger that sends a request to an API endpoint                                                |
| **Generic webhook**              | Webhook type supported by the source                                                           |
| **GitHub webhook**               | Common webhook that can trigger from repository events                                         |
| **Image change trigger**         | Trigger that starts builds when a new image version is available                               |
| **Configuration change trigger** | Trigger that starts a build when a new BuildConfig resource is created                         |
| **Source-to-Image (S2I)**        | Strategy for building reproducible images by combining a builder image with application source |
| **Builder image**                | Image containing logic used to transform inputs into outputs                                   |
| **Docker build strategy**        | Strategy requiring a repository with a Dockerfile and necessary artifacts                      |
| **Custom build strategy**        | Strategy requiring a user-created builder image                                                |
| **External artifact**            | External content supplied as build input                                                       |
| **Input secret**                 | Secret supplied as a build input                                                               |
| **PostCommit hook**              | Optional build hook defined in the `postCommit` section                                        |
| **CI/CD**                        | Continuous Integration and Continuous Delivery automation throughout the container lifecycle   |
| **Build output**                 | Resultant object, commonly a container image in this lesson                                    |

## Command Reference

### Docker

| Command        | Purpose                                            | Syntax / Example | Notes |
| -------------- | -------------------------------------------------- | ---------------- | ----- |
| `docker build` | Invoked by OpenShift for the Docker build strategy | \`\`\`bash       |       |
| docker build   |                                                    |                  |       |

````|

### Build Hook / Script

| Command | Purpose | Syntax / Example | Notes |
|---|---|---|---|
| `bundle exec rake test` | Visible `postCommit` test hook in the sample BuildConfig | ```bash
bundle exec rake test
``` | Shown in the video’s BuildConfig example |

> **Note:** The lesson discusses GitHub webhooks, API endpoints, Docker environment variables, Docker build arguments, and other mechanisms, but it does not provide additional executable command syntax for them.

## Source Notes

### Source Agreement

The TXT and VTT transcripts match exactly after whitespace normalization:

- TXT: **84 lines**.
- VTT: **102 cues**.
- Normalized transcript: **exact match**.

### Source / Video Differences

The video adds visual presentation details that are not fully represented as prose in the transcript, including:

- The “What you will learn” icon layout.
- The ImageStream registry/tag diagram.
- The S2I flow diagram.
- The BuildConfig YAML sample.
- The Docker build strategy comparison layout.
- The custom-build visual.
- The CI/CD arrow sequence.

These visual elements are referenced with screenshots above rather than duplicated as prose when the screenshot itself preserves the information.

### Ambiguous or Low-Resolution Items

> ⚠️ **Unclear in source/video:** The spoken description of `runPolicy` values is transcribed as “default, serial, or sequentially and simultaneously.” The visual sample shows `runPolicy: "Serial"`. No external correction has been applied.

> ⚠️ **Unclear in source/video:** The exact punctuation/formatting of some fields in the low-resolution BuildConfig YAML cannot be verified with complete confidence. The visible names and values are transcribed where readable, and the original frame is provided for reference.

### Terminology Fidelity

The source terminology is preserved, including:

- “build config”
- “ImageStream”
- “image change trigger”
- “configuration change trigger”
- “source-to-image”
- “custom build”
- “custom builder image”
- “postCommit”
- “CI/CD”
- “bundle exec rake test”

## Complete Cleaned Transcript

The following is the complete substantive spoken content from the TXT/VTT sources, cleaned of subtitle segmentation and filler while retaining the full meaning and source order.

```text
Welcome to Builds. After watching this video, you will be able to describe what a build is, build input sources and build strategy; describe what image streams do and identify their features; explain how to automate builds using build triggers; list the steps used for the BuildConfig process; and explain Source-to-Image, Docker, and custom build strategies.

A build is the process of transforming inputs into a resultant object, for example, transforming source code to a container image. A build requires a build configuration file or BuildConfig, which defines the build strategy and input sources.

Commonly used build strategies are Source-to-Image, or S2I, Docker, and custom.

A build input source provides content for builds. You can use the following build inputs listed in order of precedence: inline Dockerfile definitions, content extracted from existing images, Git repositories, binary or local inputs, input secrets, and external artifacts.

Multiple inputs can be combined into a single build, and an inline Dockerfile takes precedence and overwrites any external Dockerfile.

An ImageStream is an abstraction for referencing container images within OpenShift. An ImageStream continuously creates and updates container images, but does not contain actual image data. Instead, it points to images stored in internal and external registries or to other ImageStreams.

A single ImageStream can consist of many different tags, such as latest, dev, and test, and each tag points to a certain image in a registry.

To deploy an application, you refer to the ImageStream tag rather than hardcode the registry URL and tag. If the source image location changes, you update the ImageStream definition rather than individually updating all the deployments.

An ImageStream also provides a trigger capability that automatically invokes builds and deployments when a new version of an image is available.

Rather than running builds manually, automate the process using triggers. Webhook triggers send a request to an API endpoint, and they also support generic webhooks and the more often used GitHub webhooks, which send the trigger request to the API endpoint on any new commit or a pull request or other circumstances.

Next is the image change trigger, which triggers builds when a new version of an image is available. For instance, if you build your application using a Node.js base image, that image is updated when security fixes are released and other updates occur.

Finally, a configuration change trigger causes a new build to run when you create a new BuildConfig resource.

Let's look at a sample configuration file for BuildConfig. The specification creates a new BuildConfig named Ruby Sample build. The run policy field controls how builds created from a build configuration need to run. Values include the default, serial, or sequentially and simultaneously. You can also specify a list of triggers that creates a new build.

The source section defines the build's source, and the source type determines the primary input, like a Git repository, an inline Dockerfile, or binary payloads.

The strategy section shows which strategy was used to execute the build, such as source, Docker, or custom strategy.

This example uses the ruby-20-centos7 container image and Source-to-Image, or S2I, strategy for the application build.

After you build the container image, it is pushed into the repository described in the output section, and the postCommit section defines an optional build hook.

Another build strategy offered by OpenShift is called Source-to-Image, or S2I. The S2I tool builds reproducible container images and injects a container image with the app source to produce a ready-to-run image.

The new image is built by incorporating a builder image plus the source that avoids using a Dockerfile, which enables going from source-to-image in a single step.

OpenShift comes with a variety of available builder images, saving you time and development effort.

Using a Docker build strategy requires a repository that contains a Dockerfile and the necessary artifacts. When you kick off a build, OpenShift takes the input, invokes the Docker build command, and creates an image, which is then pushed to the internal OpenShift registry.

Here are four ways to implement the Docker build strategy: replace Dockerfile from image, use Dockerfile path, use Docker environment variables, or add Docker build arguments.

In a custom build strategy, you must define and create your own builder image required for the build process.

Custom builder images are regular Docker images that contain the logic needed to transform the inputs into the expected outputs.

Both Docker and S2I strategies result in runnable images, but the custom build strategy creates additional objects like JAR files and CI/CD deployment that performs unit or integration tests.

Custom builds are only available to cluster administrators because they run with high privileges.

Cloud-native development requires greater automation throughout the container lifecycle. Automation is available using the Continuous Integration and Continuous Delivery pipeline, or CI/CD.

For example, the OpenShift CI/CD process automatically merges new code requests to the repository, then builds, tests, approves, and deploys a new version to different environments.

In this video, you learned that a build is a process that transforms inputs into an object.

Build inputs in order of precedence include inline Dockerfile definitions, content extracted from existing images, Git repositories, binary or local inputs, input secrets, and external artifacts.

An ImageStream is an abstraction for referencing container images within OpenShift.

You can automate builds using a webhook, image change, or configuration change trigger.

Commonly used build strategies include Source-to-Image, or S2I, Docker, and custom build strategies.

And finally, builds require a build configuration file or BuildConfig, which defines the build strategy and input sources.
````

## VTT Timing Index

The VTT contains **102 timed cues**. The transcript content is preserved above; the timing information below provides navigation by lesson section.

| Approximate time | Topic                     |
| ---------------- | ------------------------- |
| 00:00–00:40      | Learning objectives       |
| 00:40–01:05      | What is a build           |
| 01:05–01:35      | Build input sources       |
| 01:35–02:20      | ImageStreams              |
| 02:20–03:15      | Build triggers            |
| 03:15–04:25      | BuildConfig process       |
| 04:25–05:05      | S2I                       |
| 05:05–05:35      | Docker build strategy     |
| 05:35–06:05      | Custom build strategy     |
| 06:05–06:40      | Builds automation / CI/CD |
| 06:40–07:25      | Recap                     |

### Source Statistics

```
TXT lines: 84
VTT cues: 102
TXT/VTT normalized transcript: exact match
Video duration: 445.3 seconds
```

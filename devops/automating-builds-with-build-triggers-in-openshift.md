# Automating Builds with Build Triggers in OpenShift

## Overview

Build triggers start OpenShift builds when defined events occur. They remove manual build starts and help keep application images current.

## Learning objectives

After completing this lesson, you can:

1. Explain the purpose of build triggers.
2. Identify webhook, image change, and configuration change triggers.
3. Describe the event that starts each trigger type.

## Build triggers

A build trigger automatically starts a build when an event occurs. Configure triggers in a `BuildConfig` to automate builds from source updates, image updates, or configuration changes.

| Trigger              | Event                                         | Result                                  |
| -------------------- | --------------------------------------------- | --------------------------------------- |
| Webhook              | An external service sends an HTTP request     | Starts a build                          |
| Image change         | A new version of a watched image is available | Rebuilds with the updated image         |
| Configuration change | A `BuildConfig` is created or changed         | Starts a build using that configuration |

## Webhook triggers

A webhook trigger exposes an OpenShift endpoint that accepts HTTP `POST` requests. Source-control services can call this endpoint after repository events, such as a commit or pull request.

OpenShift supports generic and GitHub webhook triggers. Use a webhook trigger when your build should respond to an external event.

![Webhook trigger workflow](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/_a52f6888cac84f929bce96017e600822_Workflow-Trigger.png?expiry=1791456228218\&hmac=cnasvFCdA4e3OZ2uMflnkL5FEj0INITbVQQXqirHI0c)

### Workflow

1. A developer pushes code to a repository.
2. The repository sends a `POST` request to the webhook endpoint.
3. OpenShift receives the request and starts a build.
4. The build produces an updated application image.

## Image change triggers

An image change trigger starts a build when a new version of a watched container image becomes available. Use it when a build depends on a base or builder image.

For example, an application using a Node.js builder image can rebuild after a new image version includes security fixes. The resulting application image then includes the updated base image.

![Image change trigger workflow](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/_67b270f358f340bd81655a595e06a61a_Image-Change-Triggers.png?expiry=1791456228218\&hmac=yRPoN573LBnjmfPtgzlVbUa4-jNQXNIAtB7Fuk_fFSc)

### Workflow

1. A new base-image version is pushed to a registry.
2. The image change trigger detects the new version.
3. OpenShift starts a build with the updated image.
4. The build produces an updated application image.

## Configuration change triggers

A configuration change trigger starts a build when a `BuildConfig` is created or updated. It ensures the build reflects changes to its configuration.

Configuration changes can include the source repository, build strategy, or output destination. Use this trigger when configuration updates should take effect immediately.

![Configuration change trigger workflow](https://d3c33hcgiwev3.cloudfront.net/imageAssetProxy.v1/_33aece26af254a04b392537bfe416093_Configuration-Change-Triggers.png?expiry=1791456228218\&hmac=yHj58tX8myEuAuSXtzKKXBj0jA13DR75WgvKw_uhq6Q)

### Workflow

1. A `BuildConfig` is created or updated.
2. The configuration change trigger detects the change.
3. OpenShift starts a build using the updated configuration.
4. The build produces an updated application image.

## Summary

Use build triggers to automate builds around the events that matter:

* **Webhook triggers** respond to external HTTP requests.
* **Image change triggers** respond to new container image versions.
* **Configuration change triggers** respond to `BuildConfig` changes.

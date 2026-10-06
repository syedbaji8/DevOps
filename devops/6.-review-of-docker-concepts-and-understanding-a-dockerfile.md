# Review of Docker Concepts and Understanding a Dockerfile

This reading is designed to enhance your understanding of Docker concepts and guide you through the process of comprehending a Dockerfile.

#### Reading Overview:

* **Docker Concepts**
* **Understanding a Dockerfile**

#### Docker Concepts

**Overview**

Docker simplifies the process of creating, deploying, and managing applications by using containers. Containers allow you to package an application with its dependencies into a standardized unit for software development. Docker provides tools and a platform to build, ship, and run containers across various environments.

**Dockerfile**

A text file that contains instructions for building a Docker image. It specifies the base image, sets the working directory, installs dependencies, copies application code, exposes ports, and defines commands to run the application.

**Container**

An instance of a Docker image that runs as a process on the host machine. Containers are lightweight, portable, and isolated, making them ideal for deploying and scaling applications.

**Docker Image Storage**

Docker images are stored in registries, which can be public or private. Public registries like Docker Hub host millions of images, while organizations often use private registries for security and control.

**Where Docker Images Exist**

**Local Machine:** When you build a Docker image, it's initially stored locally on your machine. You can list local Docker images using the docker images command.

**Registry:** After building, you can push Docker images to a registry, making them accessible from anywhere with access to that registry.

#### Dockerfile

Below is a sample Dockerfile for reference. The subsequent explanation details the commands used, providing a comprehensive understanding of how to write a Dockerfile.

{% code overflow="wrap" %}
```docker
# Use an official OpenJDK 21 image as the base image
FROM openjdk:21-jdk-slim

# Set a working directory inside the container
WORKDIR /app

# Label the image with metadata
LABEL maintainer="Your Name <your.email@example.com>"
LABEL version="1.0"
LABEL description="A Java web application running in Docker"

# Copy the compiled JAR file to the container
COPY target/myapp.jar /app/myapp.jar

# Expose port 8080 to allow external access
EXPOSE 8080

# Run the application when the container starts
CMD ["java", "-jar", "/app/myapp.jar"]

# Health check to ensure the application is running
HEALTHCHECK --interval=30s --timeout=10s --start-period=10s --retries=3 \
    CMD curl --fail http://localhost:8080/health || exit 1
```
{% endcode %}

#### Understanding the Dockerfile

**1: Base Image**

Uses FROM openjdk:21-jdk-slim, which provides Java 21.

**2: Working Directory**

Sets /app as the working directory.

**3: Labeling the Image**

Adds metadata like maintainer name, version, and description.

**4: Copying the Application**

Copies myapp.jar (your Java web application) into the container.

**5: Exposing Port 8080**

Allows traffic to reach the application.

**6: Running the Application**

`CMD` runs the Java application using `java -jar`.

**7: Health Check**

Checks if the app is running at [http://localhost:8080/health](http://localhost:8080/health). If the request fails, Docker marks the container as unhealthy. Runs every 30s with 3 retries if the check fails.

#### Build the Docker Image

{% code overflow="wrap" %}
```bash
docker build -t my-java-app .
```
{% endcode %}

#### Run the Container

{% code overflow="wrap" %}
```bash
docker run -p 8080:8080 my-java-app
```
{% endcode %}

#### Check Container Health

{% code overflow="wrap" %}
```bash
docker ps --filter "health=unhealthy"
```
{% endcode %}

#### Summary

In this reading, you learned about Docker concepts and the process of creating a Dockerfile. The provided Dockerfile and the outlined steps demonstrate how to build a Docker image for a Java application. It starts with a JDK 21 base image, defines a working directory, sets up environment variables. The application code is then copied into the container, and a health check is included to ensure the container runs correctly.

<br>

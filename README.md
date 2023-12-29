## What is Docker?

Docker is a platform designed to streamline the deployment of applications by encapsulating them within lightweight, portable containers. These containers operate as self-sufficient units, running applications and their dependencies in isolation from the host system.

## How is it different from a Virtual Machine?

Docker containers differ from traditional virtual machines (VMs) as they share the host operating system's kernel, making them more lightweight and efficient. Unlike VMs, which require a full operating system for each instance, Docker containers run on a shared OS, resulting in quicker startup times and reduced resource consumption.

## What is a Container?

Containers are lightweight, standalone, and executable packages encompassing everything required to run a piece of software. This includes the code, runtime, libraries, and system tools. Containers ensure consistency across different environments, guaranteeing reliable application execution on any system.

## How to Install Docker

To install Docker, follow these steps:

1. **Linux:**
   - For Debian/Ubuntu-based systems:
     ```bash
     sudo apt-get update
     sudo apt-get install docker-ce docker-ce-cli containerd.io
     ```
   - For Fedora:
     ```bash
     sudo dnf install docker
     ```

2. **Windows and Mac:**
   - Download and run the Docker Desktop installer from [Docker's official website](https://www.docker.com/products/docker-desktop).

## Checking Docker Version

After installation, verify your Docker version using the following command:

```powershell
docker version
```

Run this command in your PowerShell or Windows Command Prompt to display information about the Docker client and server versions installed on your system.

---

## Development Workflow

In a Dockerized development workflow, the key component is the Dockerfile. This file contains instructions for Docker to create an image that encapsulates everything needed for your application's execution. Typically, a Docker image includes a streamlined operating system, a runtime environment (e.g., Node.js), application files, third-party libraries, and environment variables.

### Dockerfile Example:

```dockerfile
# Use an official base image
FROM node:14-alpine

# Set the working directory
WORKDIR /app

# Copy package.json and package-lock.json to the working directory
COPY package*.json ./

# Install app dependencies
RUN npm install

# Copy application files to the working directory
COPY . .

# Expose a port, if applicable
EXPOSE 3000

# Define the command to run your application
CMD ["npm", "start"]
```

To create an image, run:

```bash
docker build -t your-app-image .
```

### Running the Application in a Container:

Start a container and run your application:

```bash
docker run -p 3000:3000 -d your-app-image
```

This command maps port 3000 from the container to port 3000 on your local machine (`-p 3000:3000`) and runs the container in detached mode (`-d`).

---

## Docker in Action

Let's set up a basic project:

```bash
mkdir LearningDocker
cd LearningDocker
code .
```

Create an `app.js` file with the following code:

```javascript
console.log("Hello, world!");
```

Run the application locally:

```bash
node app.js
```

Now, let's create a `Dockerfile` with the following commands:

```dockerfile
FROM node:alpine

COPY . /app

WORKDIR /app

CMD node app.js
```

Build the Docker image:

```bash
docker build -t learning-docker-app .
```

This process starts with a base image, installs Node.js, copies application files, and sets up the command to run the application.

Now, your application is encapsulated in a Docker image. This image can be pushed to a registry like Docker Hub and pulled onto any machine with Docker installed. The deployment process becomes consistent and simplified, eliminating the need for complex release documents.

To check image list run this command:

```
docker image ls
```

now you can run the image on different computer and devices, just run this command

``` docker run LearningDocker ```

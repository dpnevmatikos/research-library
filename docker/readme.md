# Concepts

### Basic
1. **Container**: A running process isolated from its' host.
1. **Image**: A private filesystem provided for the `Container` to run on.
Images include everything the `Container` requires to run `Application`.
(the code or binary, runtimes, dependencies, and any other filesystem objects required)
1. **DockerFile**: describes how to assemble a private filesystem for a container, and can also contain some metadata describing how to run a container based on this image.
1. **Docker-compose.yml**: orchestrates how the containers' will run, and composes
multiple commands to a single file ([source](https://docs.docker.com/compose/gettingstarted/#step-3-define-services-in-a-compose-file))


# Usage

## Steps to render a Nodejs app

1. Create a `container` with a `DockerFile` ([source](https://docs.docker.com/get-started/part2/#define-a-container-with-dockerfile)): 

```docker
# Use the official image as a parent image
FROM node:current-slim

# Set the working directory
WORKDIR /usr/src/app

# Copy the file from your host to your current location
COPY package.json .

# Run the command inside your image filesystem
RUN npm install

# Inform Docker that the container is listening on the specified port at runtime.
EXPOSE 8080

# Run the specified command within the container.
CMD [ "npm", "start" ]

# Copy the rest of your app's source code from your host to your image filesystem.
COPY . .
```

2. Build the image:

```docker
docker build --tag bulletinboard:1.0 .
```

2. Run the image as a container ([source](https://docs.docker.com/get-started/part2/#run-your-image-as-a-container)):
```docker
docker run --publish 8000:8080 --detach --name bb bulletinboard:1.0
```

## .NET Development workflow for Docker apps
1. [Development workflow for Docker apps](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/docker-application-development-process/docker-app-development-workflow)

## Useful commands
1. `docker image ls`: list available images
1. `docker image rm <container's name or id>`: delete an image
1. `docker logs <container's name or id>`: show output from a container
1. `docker exec -it <container's name> sh` : a shell into the container's 
filesystem.


# Code samples

# Infrastructure
1. [Download](https://docs.docker.com/get-started/#download-and-install-docker-desktop)

# Use cases
1. Software Development
    - Easy installation of dev server for databases, apps etc.



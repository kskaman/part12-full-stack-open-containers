# Docker Essentials: Definitions, Commands, and Flags

This guide provides a quick reference for fundamental Docker concepts and command-line operations.

## Core Definitions

* **Image**: A read-only, immutable template containing your application code, dependencies, system tools, and instructions on how to run the application. Think of it as a blueprint or a "pre-cooked" package.
* **Container**: A runnable instance of an image. It's a live, isolated environment where your application executes. Containers are dynamic and ephemeral, while images are static.
* **Docker Engine**: The core background service (daemon) that builds, runs, and manages Docker images and containers on your host machine.
* **Docker Client**: The command-line interface (CLI) tool you use to interact with the Docker Engine (daemon).
* **Docker Hub**: A public cloud-based registry service for sharing and finding Docker images.
* **Docker Compose**: A tool for defining and running multi-container Docker applications. It uses a YAML file to configure application services, allowing them to be run with a single command.
* **Layer**: A read-only filesystem change in a Docker image. Each instruction in a Dockerfile (used to build images) creates a new layer, promoting efficiency and reusability.
* **Tag**: A label used to differentiate versions of a Docker image (e.g., `node:20`, `ubuntu:latest`).

## Essential Docker Commands

### `docker -v`

* **Meaning**: Displays the installed Docker version.
* **Usage**: `docker -v`

### `docker container run [OPTIONS] IMAGE [COMMAND] [ARG...]`

* **Meaning**: Creates and starts a new container from a specified image. If the image is not found locally, Docker will attempt to pull it from Docker Hub.
* **Usage**:
    * `docker container run hello-world` (Runs a simple "hello-world" container)
    * `docker container run -it ubuntu bash` (Starts an interactive bash session in an Ubuntu container)
    * `docker container run --rm --name my-temp-app my-custom-image` (Runs a named container and removes it upon exit)

### `docker image pull IMAGE`

* **Meaning**: Downloads an image from a registry (like Docker Hub) to your local machine.
* **Usage**: `docker image pull ubuntu:latest`

### `docker container ls` or `docker ps`

* **Meaning**: Lists all *running* Docker containers.
* **Usage**: `docker container ls` or `docker ps`

### `docker container ls -a` or `docker ps -a`

* **Meaning**: Lists *all* Docker containers, including those that are stopped or exited.
* **Usage**: `docker container ls -a` or `docker ps -a`

### `docker start CONTAINER-ID-OR-CONTAINER-NAME`

* **Meaning**: Starts one or more stopped containers.
* **Usage**:
    * `docker start my-ubuntu-container`
    * `docker start -i my-interactive-container` (Starts and attaches interactively)

### `docker kill CONTAINER-ID-OR-CONTAINER-NAME`

* **Meaning**: Forcefully stops a running container by sending a `SIGKILL` signal to its main process.
* **Usage**: `docker kill my-running-app`

### `docker container rm CONTAINER-ID-OR-CONTAINER-NAME`

* **Meaning**: Removes one or more stopped containers. You cannot remove a running container unless you use the `-f` (force) flag.
* **Usage**: `docker container rm old-container-id`

### `docker commit CONTAINER-ID-OR-CONTAINER-NAME NEW-IMAGE-NAME`

* **Meaning**: Creates a new image from the changes made to a running container. This saves the container's current state as a reusable image.
* **Usage**: `docker commit my-modified-ubuntu my-ubuntu-with-node`

### `docker image ls`

* **Meaning**: Lists all Docker images stored on your local machine.
* **Usage**: `docker image ls`

### `docker container cp SOURCE_PATH DESTINATION_PATH`

* **Meaning**: Copies files/folders between a container and the local filesystem.
* **Usage**:
    * **Host to Container**: `docker container cp ./local-file.txt my-container:/app/container-file.txt`
    * **Container to Host**: `docker container cp my-container:/app/output.log ./local-output.log`

## Important Docker Flags

* **`-a` or `--all`**
    * **Used with**: `docker container ls` (`docker ps`)
    * **Meaning**: Shows all containers, including those that have exited. Without it, only running containers are displayed.
    * **Example**: `docker ps -a`

* **`-i` or `--interactive`**
    * **Used with**: `docker container run`, `docker start`
    * **Meaning**: Keeps `STDIN` (standard input) open, allowing you to interact with the container's shell or process.
    * **Example**: `docker run -i ubuntu bash`

* **`-t` or `--tty`**
    * **Used with**: `docker container run`
    * **Meaning**: Allocates a pseudo-TTY (pseudo-terminal) for the container. This provides a more traditional and user-friendly command-line experience. Often used with `-i`.
    * **Example**: `docker run -it ubuntu bash` (Commonly combined with `-i`)

* **`--name NAME`**
    * **Used with**: `docker container run`
    * **Meaning**: Assigns a custom, human-readable name to your container. If omitted, Docker generates a random name.
    * **Example**: `docker run --name my-web-app my-app-image`

* **`--rm`**
    * **Used with**: `docker container run`
    * **Meaning**: Automatically removes the container's filesystem when the container exits. Useful for temporary or single-use containers.
    * **Example**: `docker run --rm ubuntu ls`

* **`-f` or `--force`**
    * **Used with**: `docker container rm`, `docker stop`, `docker kill`
    * **Meaning**: Forces the action, typically allowing removal of running containers (for `rm`) or a faster stop/kill.
    * **Example**: `docker rm -f my-stuck-container` (Forcefully removes a running container)
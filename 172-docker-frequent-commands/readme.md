Here’s a list of frequently used Docker commands with explanations:

### 1. `docker --version`

- **Explanation**: Displays the installed version of Docker.

### 2. `docker pull <image-name>`

- **Explanation**: Downloads a Docker image from a Docker registry (e.g., Docker Hub) to your local machine.
- **Example**: `docker pull ubuntu` pulls the Ubuntu image from Docker Hub.

### 3. `docker images`

- **Explanation**: Lists all Docker images available on your local machine.

### 4. `docker run <image-name>`

- **Explanation**: Runs a container from a Docker image. If the image is not available locally, Docker will pull it first.
- **Options**:
  - `-it`: Run the container interactively (useful for interactive terminals).
  - `--name <container-name>`: Assign a name to the container.
  - `-d`: Run the container in detached mode (in the background).
  - `-p <host-port>:<container-port>`: Maps the container’s port to a port on the host machine.
- **Example**: `docker run -it ubuntu` runs an interactive Ubuntu container.

### 5. `docker ps`

- **Explanation**: Lists currently running Docker containers.
- **Options**:
  - `-a`: Lists all containers, including stopped ones.

### 6. `docker exec -it <container-name> <command>`

- **Explanation**: Executes a command inside a running container.
- **Example**: `docker exec -it my-container bash` starts a bash session inside a running container.

### 7. `docker stop <container-name>`

- **Explanation**: Stops a running container.
- **Example**: `docker stop my-container` stops the container named "my-container."

### 8. `docker rm <container-name>`

- **Explanation**: Removes a stopped container.
- **Example**: `docker rm my-container` deletes the container "my-container."

### 9. `docker rmi <image-name>`

- **Explanation**: Removes a Docker image from your local machine.
- **Example**: `docker rmi ubuntu` removes the Ubuntu image.

### 10. `docker build -t <tag-name> <path>`

- **Explanation**: Builds a Docker image from a `Dockerfile`.
- **Options**:
  - `-t <tag-name>`: Tags the image with a name.
- **Example**: `docker build -t my-app .` builds an image from the current directory and tags it as "my-app."

### 11. `docker logs <container-name>`

- **Explanation**: Fetches and displays the logs of a running or stopped container.
- **Example**: `docker logs my-container` shows the logs for "my-container."

### 12. `docker-compose up`

- **Explanation**: Starts all services defined in a `docker-compose.yml` file.
- **Options**:
  - `-d`: Run the services in detached mode (in the background).
- **Example**: `docker-compose up -d` starts the services defined in the compose file in detached mode.

### 13. `docker-compose down`

- **Explanation**: Stops and removes all containers defined in a `docker-compose.yml` file.
- **Example**: `docker-compose down` stops and removes the services.

### 14. `docker network ls`

- **Explanation**: Lists all Docker networks.

### 15. `docker network create <network-name>`

- **Explanation**: Creates a new Docker network for containers to communicate.
- **Example**: `docker network create my-network` creates a custom network named "my-network."

### 16. `docker volume ls`

- **Explanation**: Lists all Docker volumes.

### 17. `docker volume create <volume-name>`

- **Explanation**: Creates a new Docker volume.
- **Example**: `docker volume create my-volume` creates a volume named "my-volume."

### 18. `docker inspect <container-name/image-name>`

- **Explanation**: Displays detailed information about a container or image in JSON format.
- **Example**: `docker inspect my-container` provides information about the "my-container."

### 19. `docker tag <source-image> <target-image>`

- **Explanation**: Adds a new tag to an existing image.
- **Example**: `docker tag ubuntu:latest myrepo/ubuntu:v1` tags the "ubuntu:latest" image as "myrepo/ubuntu:v1."

### 20. `docker push <image-name>`

- **Explanation**: Pushes a tagged image to a Docker registry (e.g., Docker Hub).
- **Example**: `docker push myrepo/ubuntu:v1` pushes the "myrepo/ubuntu:v1" image to Docker Hub.

These commands cover essential Docker operations, from managing containers and images to working with networks and volumes.

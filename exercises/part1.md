# Part 1 Exercises

## 1.1 Getting Started

### Assignment

> Since we already did “Hello, World!” in the material let’s do something else.
> Start 3 containers from image that does not automatically exit, such as nginx, detached.
> Stop 2 of the containers leaving 1 up.
> Submitting the output for docker ps -a is enough to prove this exercise has been done.

### Solution

1. Run three detached containers

   ```sh
   docker run -d nginx
   docker run -d prom/prometheus
   docker run -d -e POSTGRES_PASSWORD=somepassword postgres
   ```

1. Stop one container

   ```sh
   docker stop affectionate_volhard
   ```

1. List running containers

   ```sh
   docker container ls
   # outputs =>
   # CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS               NAMES
   # 692f8c963de3        prom/prometheus     "/bin/prometheus --c…"   6 minutes ago       Up 6 minutes        9090/tcp            serene_greider
   # 930f34633354        nginx               "nginx -g 'daemon of…"   6 minutes ago       Up 6 minutes        80/tcp              cocky_vaughan
   ```

## 1.2 Cleanup

### Assignment

> We’ve left containers and a image that won’t be used anymore and are taking space, as `docker ps -as` and `docker images` will reveal.
> Clean the docker daemon from all images and containers.
> Submit the output for docker ps -a and docker images

### Solution

- Containers

  ```sh
  # list containers
  docker container ls -a

  # stop running containers
  docker stop 9c 34 1d

  # remove containers
  docker container prune

  # list containers
  docker container ls -a #outputs:
  # CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
  # ~
  ```

- Images

  ```sh
  # list images
  docker images

  # all images
  docker rmi $(docker images -aq)

  # list images
  docker images #outputs:
  # REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
  # ~
  ```

## 1.3 Hello Docker Hub

### Assignment

> Start image devopsdockeruh/pull_exercise with flags -it like so: docker run -it devopsdockeruh/pull_exercise. It will wait for your input. Navigate through docker hub to find the docs and Dockerfile that was used to create the image.
> Read the Dockerfile and/or docs to learn what input will get the application to answer a “secret message”.
> Submit the secret message and command(s) given to get it as your answer.

### Solution

```sh
"This is the secret message"
```

## 1.4 Enter a Running Container

### Assignment

> Now that we’ve warmed up it’s time to get inside a container while it’s running!
>
> Start image `devopsdockeruh/exec_bash_exercise`, it will start a container with clock-like features and create a log. Go inside the container and use `tail -f ./logs.txt` to follow the logs. Every 15 seconds the clock will send you a “secret message”.
>
> Submit the secret message and command(s) given as your answer.

### Solution

```sh
# Start the container
docker run -d devopsdockeruh/exec_bash_exercise

# Enter the running container
docker exec -it ${CONTAINER_NAME} bash

# View the logs
tail -f ./logs.txt

## OUTPUTS!
Secret message is:
"Docker is easy"
```

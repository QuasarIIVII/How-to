# How to run Docker in Docker (DinD)
this page assumes:
- you have a running docker daemon on the host
- you have the permission to run docker commands

## Step 1: Pull the DinD image
```bash
docker pull docker:dind
```

## Step 2: Run the DinD container and Access it.
```bash
docker run -d --privileged --name <container name> [-p external_port:internal_port] docker:dind
```
- `docker run` runs a container.
- `-d` runs the container in the background.
- `--privileged` gives the container full access to the host's devices. (Required for DinD)
- `--name` is the name you want to give to the container.
- `-p` is optional, it maps the container's port to the host's port.

```bash
docker exec -it <container name> sh
```
- `docker exec` runs a command inside a running container.
- `-i` keeps the STDIN open.
- `-t` allocates a pseudo-TTY.

now inside the container, you can run docker commands as you would on the host.
run `docker info` to verify that you are running docker inside the container.

## Step 3: Run a container inside the DinD container
*the shell commands from here on are run inside the DinD container.*<br>
let's run a ubuntu container inside the DinD container.
```sh
docker run -it ubuntu
```
you should now be inside the ubuntu container running inside the DinD container.

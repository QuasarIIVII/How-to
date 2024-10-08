# How to transfer a docker image in a docker container to another host
this page assumes:
- you have a running docker daemon on the host
- you have the permission to run docker commands
- you have a DinD container running on the host
    - if you don't have a DinD container running, follow the steps in '[How to run Docker in Docker (DinD)](How-to-run-Docker-in-Docker-DinD.md)'

**Run on the DinD container:**
follow `Step 1` from '[How to transfer a docker image to another host](How-to-transfer-a-docker-image-to-another-host.md)' to save the image to a tar file and return here just before `Step 2`.

## Copy the tar file
**Run on the host of the DinD container:**
<br>
```bash
docker cp <container name>:<file name>.tar <destination path>
```
- `docker cp` copies files/folders between a container and the host.
- `<container name>` is the name of the container where the tar file is saved.
- `<file name>.tar` is the name of the tar file you want to copy.
- `<destination path>` is the path where you want to save the tar file on the host.

return to `Step 2` from '[How to transfer a docker image to another host](How-to-transfer-a-docker-image-to-another-host.md)' and continue from there.

## Alternative: Transfer the tar file using `nc` (netcat)
**This way does NOT natively support SECURE transfer, use it at your own risk**
<br><br>
first, you need to install `netcat` on the DinD container.
<br>
**Run on the DinD container:**
<br>
```bash
apk add --no-cache netcat-openbsd
```
- `apk add` installs packages on Alpine Linux.
- `--no-cache` prevents apk from caching the index locally.

ensure that the receiver also has `netcat` installed.
and then, return to `Step 2 - Alternative 2` from '[How to transfer a docker image to another host](How-to-transfer-a-docker-image-to-another-host.md)' and continue from there.

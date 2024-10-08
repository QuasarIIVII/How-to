# How to transfer a docker image to another host
this page assumes:
- you have a running docker daemon on the hosts
- you have the permission to run docker commands

#### Before you start, you can create a docker image from a running container
```bash
docker commit <container id> [image name]
```

## Step 1: Save the image to a tar file
```bash
docker save -o <file name>.tar <image name>
```
You can check the saved image by running `docker images` and see if the image is listed.

## Step 2: copy the tar file to another host
### Default: rsync
```bash
rsync -avz [-e "ssh -p <port>"] <file name>.tar <user>@<receiver ip>:<destination path>
```
### Alternative 1: scp
```bash
scp -P <port> <file name>.tar <user>@<receiver ip>:<destination path>
```
### Alternative 2: nc (netcat)
**This way does NOT natively support SECURE transfer, use it at your own risk**<br><br>
**Receiver:**
```bash
nc -l -p <port> > <file name>.tar
```
**Sender:**
```bash
nc -N <receiver ip> <port> < <file name>.tar
```
Run the receiver's command first, then the sender's command.

## Step 3: Load the image on another host
```bash
docker load -i <file name>.tar
```

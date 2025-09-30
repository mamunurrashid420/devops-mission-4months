## Docker Architecture
<img src="https://github.com/mamunurrashid420/devops-mission-4months/blob/main/Linux/image/Docker_architecture.png" width="500" height="300">

## Basic Docker Commands
- `attach` Attach local standard input, output, and error streams to a running container
- `build` Build an image from a Dockerfile
- `commit` Create a new image from a container's changes
- `cp` Copy files/folders between a container and the local filesystem
- `create` Create a new container
- `diff` Inspect changes to files or directories on a container's filesystem
- `events` Get real time events from the server
- `exec` Run a command in a running container
- `export` Export a container's filesystem as a tar archive
- `history` Show the history of an image
- `images` List images
- `import` Import the contents from a tarball to create a filesystem image
- `info` Display system-wide information
- `inspect` Return low-level information on Docker objects
- `kill` Kill one or more running containers
- `load` Load an image from a tar archive or STDIN
- `login` Log in to a Docker registry
- `logout` Log out from a Docker registry
- `logs` Fetch the logs of a container
- `pause` Pause all processes within one or more containers
- `port` List port mappings or a specific mapping for the container
- `ps` List containers
- `pull` Pull an image or a repository from a registry
- `push` Push an image or a repository to a registry
- `rename` Rename a container
- `restart` Restart one or more containers
- `rm` Remove one or more containers
- `rmi` Remove one or more images
- `run` Run a command in a new container
- `save` Save one or more images to a tar archive (streamed to STDOUT by default)
- `search` Search the Docker Hub for images
- `start` Start one or more stopped containers
- `stats` Display a live stream of container(s) resource usage statistics
- `stop` Stop one or more running containers
- `tag` Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
- `top` Display the running processes of a container
- `unpause` Unpause all processes within one or more containers
- `update` Update configuration of one or more containers
- `version` Show the Docker version information
- `wait` Block until one or more containers stop, then print their exit codes
### Volume 
-  `Named volume`: docker volume create my-vol
-  `docker run -d --name devtest -v myvol2:/app nginx:latest`
-  `Anonymous volume`: docker run -d -P --name web -v /webapp training/webapp python app.py
-  `Bind mount` : docker run -d -P --name web -v /src/webapp:/opt/webapp training/webapp python app.py
- `tmpfs mount` :  docker run -d --name web -v /run --tmpfs /run:rw,noexec,nosuid,size=65536k training/webapp python app.py
### Named volume 
1. created by us
2. managed by docker
3. persist if container is deleted/remove
4. can be shared between containers
5. /var/lib/docker/volumes/
## command 
- `docker volume  create my_name_volume`
- `docker run -dit --name named_container_ex -v my_name_volume:/data alpine sh`
## Anonymous volume 
1.Create by docker 
 - dokcer run -it --name anon_volume_ex -v /data alpine sh 
 ## Bind Mount 
 - docker run -dit --name bind_mount -v  /home/ubuntu/my_data:/data alpine sh
 ## tmnfs mount
 - data stored in sensitive data(key)

### Docker Network 
## There are 5 types of networks in docker 
1. Bridge 
 - Local container network 
 - By default connected to network 
 - communication with internet via NAT( docker container)
 ```
 docker network create my_bridge
 docker network ls 
 docker network inspect my_bridge
docker run -d --name c1 --network my_bridge nginx

 ```
2. Host 
- there is  no nat or bridge 
- container host using network stack 
- container ip = host ip 
- `Limitation`: some host cannot  bind at a time  in container 
- use case: performance app , monitoring agents 
3. Overlay
- Multi-hosting Network 
- using kubernetes 
- vxlan 
4. Macvlan 
- each container isolate mac address 
- A container appears as a separate physical device on the network.
- No Nat
- Through ip in DHCP 
5. None 
- No network 
Link: https://github.com/mamunurrashid420/Docker_network_Bridge-
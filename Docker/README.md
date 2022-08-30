## What is [Docker](https://docs.docker.com/get-started/overview/) ?
- `Docker` is a container platform which has major role in making container technology so famous and widely used.
- Docker help us create, manage and control the containers.

## Docker Architecture
- Docker uses a client-server architecture.
- **Docker client:** It is the interface with we people interact. It may be `CLI` or a `GUI`.
- **Docker Host:** It listen for docker api request which we provide through `Docker client` and acts on it. Docker Daemon does this all which is a part of docker host.
- **Docker Registry:** It is cloud storage which contains all the images.
- **Docker Objects:** 
    - `Images` - It is read only templete used to create a container having the application and everything that images is specific to do.
    - `Container` - runnable instance of docker image
    - `Dockerfile` - Dockerfile is used to create an image of an application
        -  a file which contains the detailed steps to make an image and run it
        - when we change something in a dockerfile only the new layers are rebuild 
        - this makes images so lightweight and fast

## Flowpath
- We code our application
- Create a Dockerfile to make an image of our application
- start a container with Dockerfile and make an image
- publish the image
- Update the code 
- Delete the container 
- Start a new one with updated content
- publish the next version of application as image with different tags

## Basic commands and understanding
- Docker container are nothing but isolated process running its own namespace.
- We can skip the container flag when running any commands for container
- `docker version` and `docker info` are used to get info
- `docker run --help` - used to get help about flags 
- `docker container ls / docekr ps` - lists the running container
- `docker ls -a / docker ps -a ` - lists both running and stopped containers
- `docker container stop <containerId> - to stop a running container
- `docker rm -f <containerId> - to delete a container 

## Docker Containers
```bash
# start a container with image from dockerhub
docker run --detach --publish 8800:80 --name dipanshu httpd
curl localhost:8800

# list the running container
docker ps

# list all containers
docker ps -a

# check logs
docker logs <containerId>

# opening a bash shell in running container
docker exec -it <id/name> bash
hostname
exit

# pick id or name of the container and stop it
docker stop <containerId>

# list all containers
docker ps -a

# but it not deleted so,(ignore -f flag if container isn't running)
docker --rm -f <containerId>
```
## Docker Images
- `docker image ls` - lists the images present on the machine
- `docker pull nginx` - pulls an image from dockerhub in layers and if some layers already on machine then it skips that layer
- `docker image tag nginx:latest dipanshu:v1` - tagged a image and now ready to push on registry
- `docker image push dipanshu:v1` - used to push image to docker hub with correct credential entered followed on
- **just because you tag an image, doesn't mean that it changes the image ID**
- Building an image using Dockerfile
```bash
# build image (Dockerfile has to be in current dir)
docker image build -t <image-name> .
```
once the image is created than tag it and push to hub.

## Docker Volumes
- Volume are persistant storage which can be created along with container and they don't go away even if container are deleted.
- It helps us multiple containers to write and read data from same storage.
- There are two types : `Named Volume` and `Mount Volume`
- `Named volume` are volumes which we can name and can be shared by multiple container.
```bash
# create a volume with some name
docker run -d --name mysql -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -v mysql-db:/var/lib/mysql mysql

# check for the volume 
docker volume ls

# verify by going under mount for our container
docker inspect mysql 

# Now delete our container
docker rm -f mysql

# But the volume is still There
docker volume ls

# create a new container and specify it to use the previous volume
docker run -d --name mysql2 -e MYSQL_ALLOW_EMPTY_PASSWORD=yes -v mysql-db:/var/lib/mysql mysql

# check for volumes
docker volume ls
docker inspect mysql2 

```
- `Bind Mount` are used to bind volume to specific app such that in developing environment we can develop apps in real time and see the changes instead of rebuilding it again and again.
```bash
# clone a node app 
git clone https://github.com/docker/getting-started.git

# change directory
cd getting-started/app

# create a container to start the app, bind volume in the same directory and then 
# intall dependencies and start development server(sh shell because alpine don't have bash by default)
docker container run -d --name todo-app -w /app -v "$(pwd):/app" node:12-alpine sh -c "yarn install && yarn run dev"

# check logs and wait for the server to start and then go to localhost:3000
docker logs todo-app

# updating files and see changes in real time --> make some changes and go again to localhost:3000
vim src/static/js/app.js

# Now everything works fine we build and push the image to repo
docker build -t todo-app:latest todo-app:v2
docker push <username>/to-do:v2
```
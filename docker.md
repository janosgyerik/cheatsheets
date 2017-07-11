https://docs.docker.com/get-started/

```
docker ps
docker run hello-world

docker start ttrssdb
docker run -d --link ttrssdb:db -p 2000:80 clue/ttrss

# list images
docker images

# delete image
docker rmi ID

# list running containers
docker container ls

# list all containers
docker container ls -a

# delete container
docker container rm ID


```

### Build image

Create a new folder with the files to put in the image.

Create `Dockerfile` to describe how to build.

```
docker build -t somename .

# mapping machine's port 4000 to port 80 exposed with EXPOSE 80 in Dockerfile
docker run -p 4000:80 somename

# run in the background, detached
docker run -d -p 4000:80 somename

# verify it's running
docker ps

# get a new instance of a container's shell
docker exec -i -t ID /bin/bash

```

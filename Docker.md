### Basics

    # list running containers
    docker ps
    
    # run a container
    docker run hello-world
    docker run -it ubuntu bash
    docker run -it alpine sh
    
    # list images and containers
    docker image ls
    docker container ls
    
    # use --all to include no longer running
    docker container ls --all
    
    # print only ids
    docker container ls --all -q

    ## List Docker CLI commands
    docker
    docker container --help

    ## Display Docker version and info
    docker --version
    docker version
    docker info

    ## Execute Docker image
    docker run hello-world

    ## List Docker images
    docker image ls

    ## List Docker containers (running, all, all in quiet mode)
    docker container ls
    docker container ls --all
    docker container ls -aq
    
    # Build an image from current directory with Dockerfile
    # the -t option is to *tag* with a user-friendly name
    docker build -t name-for-image .
    docker image ls | head
    docker image ls name-for-image
    
    # Run the image, mapping your machine's port 4000 to the container's 80
    # the -p option is to *publish* a port
    docker run -p 4000:80 name-for-image
    
    # To stop a running container, find its id and then stop it
    docker container ls
    docker container stop the-id
    
    # Use the -d flag to run a container in detached mode, in the backround
    docker run -d -p 4000:80 friendlyhello
    
    # Publish a docker image to a registry: login, create tag, push tag
    docker login
    docker tag friendlyhello john/get-started:part2
    docker push john/get-started:part2
    
    # Pull and run image from the remote repository
    docker run -p 4000:80 username/repository:tag
    
    docker build -t friendlyhello .  # Create image using this directory's Dockerfile
    docker run -p 4000:80 friendlyhello  # Run "friendlyname" mapping port 4000 to 80
    docker run -d -p 4000:80 friendlyhello         # Same thing, but in detached mode
    docker container ls                                # List all running containers
    docker container ls -a             # List all containers, even those not running
    docker container stop <hash>           # Gracefully stop the specified container
    docker container kill <hash>         # Force shutdown of the specified container
    docker container rm <hash>        # Remove specified container from this machine
    docker container rm $(docker container ls -a -q)         # Remove all containers
    docker image ls -a                             # List all images on this machine
    docker image rm <image id>            # Remove specified image from this machine
    docker image rm $(docker image ls -a -q)   # Remove all images from this machine
    docker login             # Log in this CLI session using your Docker credentials
    docker tag <image> username/repository:tag  # Tag <image> for upload to registry
    docker push username/repository:tag            # Upload tagged image to registry
    docker run username/repository:tag                   # Run image from a registry

# Working with image

Docker image is a file, which can be store in the local file system or hosted on remote server aka docker registry. For sake of saving disk space and peformance, an image is placed on top of the other, which in turn is on top of the next one and so on.

Image can be created either 

* manually 
* automatically usimg Dockerfile

## Modify image manually

To manually modify a image, we 

* run an base image interactively using shell as command to gain access to the container console
* change the running container configuration using available command line tools e.g. `vim`
* commit the running container to a new image
* tag and push the new image to docker registry

**run**

to run an image interactively

        $ docker run -t -i --entrypoint="/bin/bash" elasticsearch-fresh:1.7

**commit**

to commit an container (i.e save container to an image)

        $ docker commit 28aa35e4f96e custwebsrv
        fea257dcf7f323e87eb83b69449645648df8a23b20287348436c3d008c8b452b

        $ docker images
        REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
        custwebsrv          latest              fea257dcf7f3        7 seconds ago       132.9 MB
        nginx               latest              a486da044a3f        6 days ago          132.9 MB

we can commit both running and stopped containers.

**tag and push**

to push image into remotr registry, we need to associate a local image with a remote image

        $docker tag elasticsearch-standalone mydocker.host.com/vertigo/elasticsearch-standalone
        
after that we can push the image

        $docker push mydocker.host.com/vertigo/elasticsearch-standalone

## Build image from Dockerfile

to build image we need to 

* prepare a folder containing `Dockerfile` with customisation instructions and other supporting files that are used in `Dockerfile` instructions
* build an image
* tag and push the new image to docker registry

**preapre**

        $ ls -l ./elasticsearch
        total 16
        -rw-r--r--  1 huyle  staff  1247 27 Aug 14:43 Dockerfile
        drwxr-xr-x  3 huyle  staff   102 27 Aug 14:43 config
        -rwxr-xr-x  1 huyle  staff   552 27 Aug 14:43 docker-entrypoint.sh

**build**

        $docker build ./elasticsearch

**tag and push**

to push image into remote registry, we need to associate a local image with a remote image
        
        $ docker images
        REPOSITORY                                             TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
        <none>                                                 <none>              7209691a599e        16 minutes ago      522.1 MB
    
        $docker tag 7209691a599e:1.7 elasticsearch-fresh
        

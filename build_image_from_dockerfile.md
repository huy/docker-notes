
# Build image from Dockerfile

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

**build and tag**

        $ docker build -t elasticsearch-fresh:1.7 elasticsearch
        Sending build context to Docker daemon 6.144 kB
        Sending build context to Docker daemon
        Step 0 : FROM java:8-jre
         ---> ff23c187d5c6
        Step 1 : RUN gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4
         ---> Running in 0b4532abdd1e        


# Docker basic

`docker` is command line interface client used to access docker daemon to operate image and container. 

**image vs container**

Docker container is instance of an image, which is light OS image without kernel, which is provided by docker host. We can create many container(s) from the same image.

Container has its own lifesycle we can start/stop container and commit i.e. save it into an image.

**workflow**

The very basic workflow is

* search for a image in a registry
* pull image from a registry
* run an image
* query containers
* commit container into an image

**search**

Ssearch for docker image using `docker search [docker-registry/]keyword` - the default docker registry is docker hub currently hosted in `hub.docker.com`

        $docker search nginx
        NAME                                  DESCRIPTION                                     STARS     OFFICIAL 
        nginx                                 Official build of Nginx.                        1260      [OK]
        jwilder/nginx-proxy                   Automated Nginx reverse proxy for docker c...   318       [OK]
        richarvey/nginx-php-fpm               Container running Nginx + PHP-FPM capable ...   63        [OK]

**pull**

pull an image from the registry

    $ docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
    elasticsearch       latest              bd58cf964c1b        3 weeks ago         514.9 MB

    $ docker pull nginx
    latest: Pulling from nginx
    aface2a79f55: Pull complete
    5dd2638d10a1: Pull complete
    97df1ddba09e: Pull complete
    
    $ docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
    nginx               latest              a486da044a3f        6 days ago          132.9 MB
    elasticsearch       latest              bd58cf964c1b        3 weeks ago         514.9 MB

**run**

run a container from the image, the `-p` public specified container port as host port 

    $ docker run -d -p 80 -p 443 a486da044a3f
    28aa35e4f96e80efa291116fa5737d980bb737a2aee06f60787271871c4547d1
  

**ps**

to show running containers

    $ docker ps
    CONTAINER ID        IMAGE                  COMMAND                CREATED             STATUS              PORTS                                              NAMES
    28aa35e4f96e        a486da044a3f           "nginx -g 'daemon of   2 minutes ago       Up 2 minutes        0.0.0.0:32810->80/tcp, 0.0.0.0:32809->443/tcp      loving_perlman

to show all containers

    $ docker ps -a
    CONTAINER ID        IMAGE                  COMMAND                CREATED             STATUS                        PORTS                                              NAMES
    28aa35e4f96e        a486da044a3f           "nginx -g 'daemon of   40 minutes ago      Up 10 minutes                 0.0.0.0:32810->80/tcp, 0.0.0.0:32809->443/tcp      loving_perlman
    96e9c48d03bf        a486da044a3f           "nginx -g 'daemon of   43 minutes ago      Exited (0) 12 minutes ago                                                        pensive_cray
**stop**

to stop an container

        $docker stop 28aa35e4f96e
        28aa35e4f96e

**commit**

to commit an container
References

* http://stackoverflow.com/questions/23735149/docker-image-vs-container

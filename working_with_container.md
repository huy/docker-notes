
# Docker client command

`docker` is command line interface client used to access docker daemon to operate image and container. 

**workflow**

The very basic workflow is

* search for a image in a remote registry
* pull image from the registry to the docker host
* run an image
* query containers
* commit container into an image
* push the image to the registry

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

sometime it is good to access to the container console to check/modify configuration, in that case, we run a image in interactive mode, allocated tty and with bash command

    $ docker run -t -i a486da044a3f bash

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

**exec**

exec command allow use to access to the container interactively

        $ docker ps
        CONTAINER ID        IMAGE                                                         COMMAND                CREATED             STATUS              PORTS                                              NAMES
        8bb22139487a        docker.atlassian.io/vertigo/elasticsearch-standalone:latest   "/docker-entrypoint.   3 hours ago         Up 3 hours          0.0.0.0:32771->9200/tcp, 0.0.0.0:32770->9300/tcp   hopeful_brown
        
        $ docker exec -it 8bb22139487a bash
        root@8bb22139487a:/# ps -ef
        UID        PID  PPID  C STIME TTY          TIME CMD
        elastic+     1     0  0 04:02 ?        00:00:45 /usr/bin/java -Xms256m -Xmx1g -D
        root        51     0  1 06:02 ?        00:00:00 bash
        root        58    51  0 06:02 ?        00:00:00 ps -ef
        root@8bb22139487a:/# exit
        

**stop**

to stop an container

        $ docker stop 28aa35e4f96e
        28aa35e4f96e

References

* http://stackoverflow.com/questions/23735149/docker-image-vs-container
* http://dghubble.com/blog/posts/docker-quicksheet/

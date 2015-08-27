# Client/server communication

Docker works in client/server fashion. Docker server aka engine aka daemon receives a command the client and execute it onbehalf. The `docker` binary includes both client and server code, which sometimes creates a confusion. 
Docker runs as daemon on a linux host. Docker client can talk with the daemon using unix socket if it runs on the same host as the daemon or remotely over TCP. The remote access is over REST API.

**the server**

Docker daemon runs as root account the unix socket it created is accessible only for root. So it relies on OS for 
security. When accessing the docker daemon remotely, docker client uses the following environment variables to determine 
which server it is going to talk to e.g.

    DOCKER_HOST=tcp://192.168.99.100:2376
    DOCKER_TLS_VERIFY=1
    DOCKER_CERT_PATH=/Users/huyle/.docker/machine/machines/dev

The presence of `DOCKER_TLS_VERIFY=1` and `DOCKER_CERT_PATH` indicate that SSL is employed for security, which 
must corresponds with the server starting with e.g.

        /usr/local/bin/docker -d -D -g /var/lib/docker -H unix:// -H tcp://0.0.0.0:2376 \
        --label provider=virtualbox \
        --tlsverify --tlscacert=/var/lib/boot2docker/ca.pem \
        --tlscert=/var/lib/boot2docker/server.pem \
        --tlskey=/var/lib/boot2docker/server-key.pem -s aufs

The client must use key signed by the same CA in order to access to the server.

**docker-machine**

Sometime we can't run docker daemon directly (e.g. on OSX) then we need kind of linux virtual machine to host the daemon, `docker-machine` is the command that is used to manage docker host - the virtual machine for docker daemon.

    $ docker-machine ls
    NAME   ACTIVE   DRIVER       STATE     URL                         SWARM
    dev    *        virtualbox   Running   tcp://192.168.99.100:2376

`docker-machine` can give us a set of environment variables required by docker client to access a docker host

    $ docker-machine env dev
    export DOCKER_TLS_VERIFY="1"
    export DOCKER_HOST="tcp://192.168.99.100:2376"
    export DOCKER_CERT_PATH="/Users/huyle/.docker/machine/machines/dev"
    export DOCKER_MACHINE_NAME="dev"
    # Run this command to configure your shell:
    # eval "$(docker-machine env dev)"
    
To ssh docker host, we can simply use 

    $docker-machine ssh dev

**the client**

`docker` binary is both client and server. The client part of `docker` is often used as primary way to control `image` and `container` but there can be different clients e.g. maven docker plugin.

**image**

Docker image is a file, which can be store in the local file system or hosted on remote server aka docker registry. For sake of saving disk space and peformance, an image is placed on top of the other, which in turn is on top of the next one and so on.

Image can be created either 

* manually 
* automatically usimg Dockerfile

**container**

Docker container is instance of an image, which is light OS image without kernel, which is provided by docker host. We can create many container(s) from the same image.

Container has its own lifesycle we can start/stop container and commit i.e. save it into an image.

References

* https://docs.docker.com/reference/api/docker_remote_api/
* https://docs.docker.com/articles/https/

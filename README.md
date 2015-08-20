# Using docker

Docker server run as daemon on a linux host. Docker client can talk with the daemon using unix socket if it runs on the same
host as the daemon or remotely over TCP.

Docker server runs as root account the unix socket it created is accessible only for root. So it relies on OS for 
security. When accessing the server remotely, docker client uses the following environment variables to determine 
which server it is going to talk to e.g.

    DOCKER_HOST=tcp://192.168.99.100:2376
    DOCKER_TLS_VERIFY=1
    DOCKER_CERT_PATH=/Users/huyle/.docker/machine/machines/dev

The presence of `DOCKER_TLS_VERIFY=1` and `DOCKER_CERT_PATH` indicate that SSL is employed for security, which 
must corresponds with the server starting with e.g.

        /usr/local/bin/docker -d -D -g /var/lib/docker -H unix:// -H tcp://0.0.0.0:2376 --label provider=virtualbox \
        --tlsverify --tlscacert=/var/lib/boot2docker/ca.pem \
        --tlscert=/var/lib/boot2docker/server.pem \
        --tlskey=/var/lib/boot2docker/server-key.pem -s aufs

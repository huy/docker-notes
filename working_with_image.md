# Working with image


**commit**

to commit an container (i.e save container to an image)

        $ docker commit 28aa35e4f96e custwebsrv
        fea257dcf7f323e87eb83b69449645648df8a23b20287348436c3d008c8b452b

        $ docker images
        REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
        custwebsrv          latest              fea257dcf7f3        7 seconds ago       132.9 MB
        nginx               latest              a486da044a3f        6 days ago          132.9 MB

we can commit both running and stopped containers.

**push**

to push image into remotr registry, we need to associate a local image with a remote image

        $docker tag elasticsearch-standalone mydocker.host.com/vertigo/elasticsearch-standalone
        
after that we can push the image

        $docker push mydocker.host.com/vertigo/elasticsearch-standalone

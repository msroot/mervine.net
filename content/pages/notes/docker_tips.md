Title: Docker Tips
Categories: notes, docker, linux

# Docker Tips

Here are a few tips that I've found useful while delving in to [Docker](https://www.docker.com/), enjoy!

**Removing images and containers in bulk.**

    :::shell
    # remove all containers
    sudo docker rm $(sudo docker ps -a -q)

    # remove all images
    sudo docker rmi $(sudo docker images -q)

    # remove image containing TERM
    sudo docker rmi $(sudo docker images | grep TERM | awk '{ print $3 }')

**Interacting with the most recent continer started.**

    :::shell
    # view last container
    sudo docker ps -l 

    # view last container sha only
    sudo docker ps -lq

    # stop, start, attach, logs, etc. last container
    #
    # $ sudo docker <action> $(sudo docker ps -lq)
    sudo docker start $(sudo docker ps -lq)
    sudo docker stop $(sudo docker ps -lq)
    sudo docker logs $(sudo docker ps -lq)
    sudo docker attach $(sudo docker ps -lq)

**Pushing to a private registry.**

    :::shell
    # assuming image 'jmervine/centos6-nodejs'
    #
    #               <current image name>    <private registry>:<port>/<image name>
    sudo docker tag jmervine/centos6-nodejs docker.myregstry.com:5000/jmervine/centos6-nodejs
    sudo docker push docker.myregstry.com:5000/jmervine/centos6-nodejs

    # I then recommend removing your old image to avoid accidentally pushing it to the public registry.
    sudo docker rmi jmervine/centos6-nodejs

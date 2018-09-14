# docker-jenkins
Jenkins Docker supporting running docker containers from within a container


* lets you run docker containers inside of docker containers (ish)
* easy to upgrade (although I roll with LTS and build internally so maybe don't pull from dockerhub)
* simple to migrate away from or to using your existing jenkins folder as `/var/jenkins_home`
* uses sockets so vertical scaling (if you want to use server IP, probably need to revisit the Dockerfile)

## Basic usage

```
docker run -d \
    --restart=always \
    --name jenkins \
    --user `echo $UID` \
    --privileged --publish 8080:8080 \
    --volume /var/run/docker.sock:/var/run/docker.sock \
    --volume $PWD/jenkins:/var/jenkins_home:z \
    -t cd2team/docker-jenkins:lts
```


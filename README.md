# docker-jenkins
Jenkins Docker supporting running docker containers from within a container

[![Build Status](https://travis-ci.org/CODESIGN2/docker-jenkins.svg?branch=main)](https://travis-ci.org/CODESIGN2/docker-jenkins)

* Lets you run docker containers inside of docker containers (ish).
* Easy to upgrade (although I roll with LTS and build internally, so maybe check what you pull from dockerhub).
* Simple to migrate away from or to using your existing jenkins folder as `/var/jenkins_home`.
* Uses sockets so vertical scaling.
  > **Note:** If you want to use server IP to horizontally-scale, you or I will probably need to revisit the Dockerfile.
  > A little-bit to mount a configuration, or provide a script with cli arguments or ENV variable

## Basic usage

```console
docker run -d \
    --restart=always \
    --name jenkins \
    --user `echo $UID` \
    --privileged --publish 8080:8080 \
    --volume /var/run/docker.sock:/var/run/docker.sock \
    --volume $PWD/jenkins:/var/jenkins_home:z \
    -t cd2team/docker-jenkins:lts
```

## Upgrading

If it's been so long that there is no compatibility with your plugins between LTS releases, I would suggest either starting afresh, or upgrading and accepting broken plugins, then using the plugin updater to upgrade them.

The benefits of using this is that you can either always use tag `lts` and `docker pull cd2team/docker-jenkins` at interval to get the latest without setting up Jenkins, docker, etc; or to pull from a specific date-time tag.

This has not been security hardened for use on the internet, it has always been used in a closed proprietary environment with a local docker registry.

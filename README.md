# docker-base-images
A collection of Dockerfiles used to build my base docker images. These images are pushed to Docker Hub
so they can later be pulled during deployment.

```
https://hub.docker.com/r/markhumphrey/
```

## Build
To build the docker image locally for testing:

```
docker build --tag="markhumphrey/python-web-runtime" python-web-runtime/
```

## Push
To push the docker image to Dockerhub

```
docker push "markhumphrey/python-web-runtime"

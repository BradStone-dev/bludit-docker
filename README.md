# Bludit Docker Image
This  is fork of Bludit Docker container repo. I changed it to use latest build of [bludit](https://github.com/bludit/bludit). Also added my Kubernetes configuration. Deployment files provided by Bludit wont work sadly, if used with more than one replica.

[![Docker Hub](https://img.shields.io/badge/Docker-Hub-blue.svg)]([https://github.com/BradStone-dev/bludit-docker)

[![Kubernetes](https://img.shields.io/badge/Kubernetes-Deployment-blue.svg)](https://github.com/BradStone-dev/bludit-docker/tree/master/kubernetes)

```
$ docker run --name bludit -p 8000:80 -d reason997/bludit-4:latest
```

To get access visit with your browser http://localhost:8000

### Run the container and mounting a volume to persist data

```
mkdir ~/bludit

docker run --name bludit \
    -p 8000:80 \
    -v ~/bludit:/usr/share/nginx/html/bl-content \
    -d reason997/bludit-4:latest
```

To get access visit with your browser http://localhost:8000

### Stop the container

```
$ docker stop bludit
```

### Delete the container

```
$ docker rm bludit
```

### Delete the image

```
$ docker rmi bludit/docker:latest
```

## Kubernetes

Run Bludit on K8s. Have to create nfs shared directory first and secret for ssl certificate.

```
$ kubectl apply -f kubernetes/pvc.yml
$ kubectl apply -f kubernetes/pv-nfs.yml
$ kubectl apply -f kubernetes/nginx-patch.yml
$ kubectl apply -f kubernetes/deployment.yml
$ kubectl apply -f kubernetes/service.yml
$ kubectl apply -f kubernetes/bludit-ingress.yml
```

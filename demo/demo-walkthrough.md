# Docker - Basics

## Docker Intro

```
cd /Users/kandasamyp/Code/k8s-demo/1.1-docker-simple

#show the docker container building
docker build .

# show the built docker images
docker images -a

#show that no containers exists
docker ps -a 
docker run -it alpine:latest

#show the hostname and the IP
cat /etc/hostname
cat /etc/hosts
exit

#show the hostname is same as container id
#docker ps -a
```

## Docker echo

```
cd /Users/kandasamyp/Code/k8s-demo/1.2-docker-echo

# show commands being run during the build
docker build . --tag alpine-pk:1.0

# show the image
docker images | grep "-pk"

# inspect the image: 
# note: Arch, OS, ContainerConfig 
docker inspect alpine-pk:1.0

# show how the image was built: go from the bottom up
docker history pkthon:1.0
``` 

## Docker nginx - mint

```
cd /Users/kandasamyp/Code/k8s-demo/1.3-nginx-server-mint

# show commands being run during the build
docker build . --tag nginx-pk:1.0

# show the image
docker images | grep "-pk"

# run the nginx container
docker run -p 8000:80 -d --host--name pkginx nginx-pk:1.0

# get the container id
docker ps -a | grep "pkginx"

#exec into a docker container | cat /etc/hosts
docker exec -it pkginx /bin/bash

# inspect the container and show how it is connected to n/w 
docker inspect pkginx 
docker network ls
docker inspect bridge
``` 


## Docker nginx - custom

```
cd /Users/kandasamyp/Code/k8s-demo/1.4-nginx-server-custom

# show commands being run during the build
docker build . --tag nginx-pk:1.0

docker images | grep "-pk"

# run the nginx container
docker run -p 8000:80 -d --name pkginx nginx-pk:1.0

# get the container id
docker ps -a | grep "pkginx"

#exec into a docker container
docker exec -it e3addedf3998 /bin/bash
``` 

# Docker - Application

## Docker Single Container App
```
cd /Users/kandasamyp/Code/k8s-demo/2.1-docker-node-bulletin-board

# build docker with tag name bulletin:1.0
docker build . --tag bulletin:1.0

# show all images and then search for bulletin
docker images | grep "bulletin"

# run the nginx container
docker run -p 8080:8080 -d --name bulletin bulletin:1.0

# get the container id
docker ps -a | grep "bulletin"
```

## Docker Orchestrating difficulties
can possibly show difficulties of managing and orchestrating with containers 

# Kubernetes - Pod

## Kubernetes - nginx single pod
```
ec
# show all pods 
kubectl get pods -A

# create a pod called nginx from nginx image listening on port 80
kubectl run nginx --image=nginx:1.16.1 --port=80

# launch interactive terminal to container
kubectl exec nginx -it /bin/bash

# inside the container
apt update && apt upgrade
cat /etc/os-release 
apt-get install curl
curl -s localhost

# opens up a proxy to kubeapi server 
kubectl proxy

#then goto 
http://127.0.0.1:8001/api/v1/namespaces/default/pods/nginx/proxy/
```

## Kubernetes - Multiple Containers per pod
```
cd /Users/kandasamyp/Code/k8s-demo/3.5-k8s-multiple-pods

k apply -f multiple-pod.yaml
k get pods -A
watchpod
kubectl exec twocontainers -t -- curl -s localhost:9876/info\n
kubectl describe pod/twocontainers -n default
```

## Kubernetes - Pod Constraints
https://kubernetesbyexample.com/pods/

# Kubernetes - Labels (help with management)
https://kubernetesbyexample.com/labels/

# Kubernetes - Deployment & Replicas

## Kubernetes - nginx deployment
```
cd /Users/kandasamyp/Code/k8s-demo/3.2-k8s-nginx-deployment

# show all pods 
kubectl get pods -A

# apply the deployment for nginx
kubectl apply -f deployment.yaml

# describe the nginx-deployment
kubectl describe deployment nginx-deployment

# show all pods 
kubectl get pods -A

# show replicaset
k get rs

# opens up a proxy to kubeapi server 
kubectl proxy  #opens up a proxy to kubeapi server 

#then goto 
http://127.0.0.1:8001/api/v1/namespaces/default/pods/<pod-name>/proxy/
```

## Kubernetes - nginx deployment update
```
cd /Users/kandasamyp/Code/k8s-demo/3.3-k8s-nginx-update

# show all pods 
kubectl get pods -A

# apply the deployment for nginx
kubectl apply -f deployment.yaml

# show replicaset
k get rs

#rollout information
kubectl rollout history deployment nginx-deployment

#roll back to revision 1
kubectl rollout undo deployment nginx-deployment --to-revision=1

# describe the nginx-deployment
kubectl describe deployment nginx-deployment

# delete the nginx-deployment
kubectl delete deployment nginx-deployment
```

# Kubernetes - Service

```
cd /Users/kandasamyp/Code/k8s-demo/3.4-k8s-nginx-service

# apply the deployment for nginx
kubectl apply -f nginx-service.yaml

# show all pods 
kubectl get pods -A

# expose the service through NodePort
#kubectl expose deployment nginx-deployment --type=NodePort --name=nginx-svc

kubectl describe services nginx-service

curl http://10.10.0.26:80
```

Done with Stateless App deploymeny

# Kubernetes - Storage

## Persistent Volumes and Claims



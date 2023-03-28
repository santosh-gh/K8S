# URL
https://www.dotnetcurry.com/tutorials/devops
https://kubernetes.io/docs/tasks/access-application-cluster/ingress-minikube/

https://devopscube.com/kubernetes-minikube-tutorial/

https://www.dotnetcurry.com/aspnet-core/kubernetes-for-developers
https://www.dotnetcurry.com/devops/1531/azure-devops-automated-terraform-cicd



Disable/Enable Hyper-V in command line

    # Enable
    bcdedit /set hypervisorlaunchtype auto

    # Disable
    bcdedit /set hypervisorlaunchtype off


minikube config set driver virtualbox
minikube config set driver docker

minikube stop
minikube delete --all
minikube start

kubectl exec -it postgres-deployment-5f88678b76-kpl8b -n default -- /bin/bash


# Example
https://k8s-examples.container-solutions.com/

# Kubectl
  kubectl cluster-info
  kubectl get nodes
  kubectl get events
  kubectl get services
  kubectl get pods
  kubectl get namespace
  kubectl get pods --namespace=kube-system
  kubectl config view
  kubectl get cs (see the Component Statuses)


# HelloWorldWebApp

  https://www.tutorialsteacher.com/core/net-core-command-line-interface

  dotnet new webapp  -n HelloWorldWebApp -f net6.0

  dotnet build .\HelloWorldWebApp\HelloWorldWebApp.csproj

  dotnet run --project .\HelloWorldWebApp\HelloWorldWebApp.csproj

# Add .gitignore file 
  Add the Extention .gitignore Generator
  In VS code Command Palette Add .gitignore
  
# Add Dockerfile and .dockerignore
  
  - Install C# extention (C# for Visual Studio Code (powered by OmniSharp))
  - Command Palette (Ctrl+Shift+P)
  - Add dockeer file to namespace


# Use a .dockerignore File

  A properly structured .dockerignore file can help:

  - Decrease the size of the Docker image
  - Speed up the build process
  - Prevent unnecessary cache invalidation
  - Prevent leaking secrets


# Docker Image
  
  docker build -t helloworldwebapp .    (Repository name must be lowercase) 

  docker run -p 5000:80  helloworldwebapp
  
# Docker Push

  docker tag helloworldwebapp  e880613/helloworldwebapp:v1 

  docker login
  docker push e880613/hellowordwebapp:v1

# minikube
  minikube version 
  minikube status

# kubectl 
  kubectl cluster-info


# Deployment to cluster
  - create deployment.yaml
  - Create Deployment 
    kubectl apply -f .\HelloWorldWebApp\Manifest\deployment.yaml


    kubectl describe po helloworldwebapp-deployment-6b4bfbfbf9-5xrnx
    kubectl run -it --rm --restart=Never busybox --image=yauritux/busybox-curl sh
    curl http://172.17.0.3


    kubectl exec -it helloworldwebapp-deployment-6b4bfbfbf9-5xrnx -- /bin/bash

    -i  represents that we want kubectl exec to run this interactive session
    -t  represents that kubectl exec should get a terminal ID allotted.

# Service 

  - ClusterIp - Using Services to allow traffic between Pods

    kubectl run -it --rm --restart=Never busybox --image=yauritux/busybox-curl sh
    curl http://helloworldwebapp-service

  - NodePort - Using NodePort services to allow external traffic
    kubectl expose deployment helloworldwebapp-deployment --port=80 --type=NodePort

    minikube service helloworldwebapp-deployment

    NodePort services are great for development and debugging, but not something you really want to depend on for your deployed applications. Every time the service is created, a random port is assigned, which could quickly become a nightmare to keep in sync with your configuration.

  - Ingress - The Ingress provides a map between a specific host name and a regular Kubernetes service.

    minikube addons enable ingress

    kubectl get pods -n ingress-nginx

# pod
  kubectl apply -f .\HelloWorldWebApp\Manifest\pod\pod.yaml
  kubectl describe pods/dotnetcoreapp-pod
  kubectl describe pods dotnetcoreapp-pod
  kubectl exec dotnetcoreapp-pod -- curl 172.17.0.3
  kubectl delete pod dotnetcoreapp-pod
  




kubectl run dotnetapp --image=e880613/dotnetcoreapp --port=80 --restart="Never" -- labels="project=demo,env=prod"
kubectl expose pod dotnetapp --port=8080 --target-port=80 --name="dotnetapp-service"


kubectl get replicasets --selector=run=pythonapp
kubectl scale deployments pythonapp-deployment --replicas=2
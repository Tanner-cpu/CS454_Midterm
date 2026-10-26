## Prerequisites
- Docker / Docker Compose
- Curl
- kubectl
- k3d
- Multipass
  
# Virtual Machine Build/Start/Access Commands 

## Create an Ubuntu VM 
multipass launch 24.04 \
  --name cs454-vm \
  --cpus 2 \
  --memory 2G \
  --disk 8G

## Enter Virtual Machine
multipass shell cs454-vm

## Start Service Inside VM
SERVICE_NAME=vm-service MESSAGE="Hello from a VM environment" node app.js

## Requests from Host 
- curl http://192.168.1.215:8080/health (status)
- curl http://192.168.1.215:8080 (simple request)

## Cleanup 
multipass delete --purge cs454-vm

# Kubernetes Build/Start/Access Commands 

## How to Build Image
docker build -t cs554-midterm  .

## How to Build Cluster 
k3d cluster create cs454 \
  --servers 1 \
  --agents 2 \
  -p "8080:80@loadbalancer"

## Import Local Image 
k3d image import cs454-midterm -c cs454

## Deploy Application 
- kubectl apply -f deployment.yaml
- kubectl apply -f service.yaml
- kubectl apply -f ingress.yaml

## Access Method (Port Forwarding)
- kubectl port-forward svc/web-service 8080:80 (listening for traffic)
- curl http://localhost:8080 (from separate terminal)

# Clean Up 
k3d cluster delete cs454

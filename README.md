## Prerequisites
- Docker / Docker Compose
- Curl
- kubectl
- k3d

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
kubectl apply -f deployment.yaml
kubectl apply -f service.yaml
kubectl apply -f ingress.yaml

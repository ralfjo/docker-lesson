# Creating a deployment configuration file

### check whether there are deployments and services create
```
kubectl get deployments
kubectl get services
minikube status
```

### create deployment file
```
# create deployment.yaml
kubectl apply -f=deployment.yaml
kubectl get deployments
kubectl get pods
```

### create service file
```
# create service.yaml
kubectl apply -f service.yaml
kubectl get services
minikube service backend
```
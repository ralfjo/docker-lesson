# Managing data and volumes with Kubernetes

### Example of volume management with Docker
```
docker-compose up -d  --build
docker ps
# http://localhost/story (get / post)

# delete docker container
docker-compose down
docker container prune

# docker start and check data
docker-compose up -d --build
# http://localhost/story (check data)
```

### Example of volume management with kubernetes
```
# write deployment.yaml, service.yaml files
# create docker hub repository
# docker image build and push
docker build -t ralf418/kub-data-demo
docker push ralf418/kub-data-demo

# minikube check
minikube status

# apply service & deployment
kubectl apply -f="service.yaml" -f="deployment.yaml"
kubectl get deployments
kubectl get services

# minikube service
minikube service story-service
```
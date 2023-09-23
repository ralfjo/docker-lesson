# kubernetes Networking

docker compose
```
docker-compose up -d --build
```

test Page
http://localhost:8080/login
- Post
- json {"email":"test@test.com", "password":"testuser"}


### kubernetes example
users app
```
# users app
# update code
# docker build
docker build -t ralf418/kub-demo-users .
docker push ralf418/kub-demo-users
```

kubernetes deployment
```
# create kubernetes directory
# make users-deployment.yaml
# deploy
kubectl apply -f users-deployment.yaml
kubectl get deployment
kubectl get pods
```

kubernetes service
```
# make users-service.yaml
# deploy
kubectl apply -f users-service.yaml
kubectl get service
```

TEST
http://127.0.0.1:53951/login
http://127.0.0.1:53951/signup
post body {email, password}


### kubernetes service ( user, auth )
```
# make auth - deploy, service yaml file
kubectl apply -f auth-service.yaml -f auth-deployment.yaml
```

### kubernetes namespace
CoreDNS
```
kubectl get namespaces
# default
```

### frontend
```
docker build -t ralf418/kub-demo-frontend .
docker run -p 80:80 --rm -d ralf418/kub-demo-frontend

# kubernetes
kubectl apply -f .\frontend-deployment.yaml -f .\frontend-service.yaml
kubectl get pods
minikube service frontend-service
```
# kubectl & deployment

```
docker build -t kub-first-app .
minikube status
kubectl create deployment first-app --image=kub-first-app
kubectl get deployments
###
# NAME        READY   UP-TO-DATE   AVAILABLE   AGE
# first-app   0/1     1            0           25s
###

kubectl get pods
###
### NAME                         READY   STATUS             RESTARTS   AGE
### first-app-6f58f94cf5-7rl6j   0/1     ImagePullBackOff   0          2m22s
# READY 0(Current State)/1(Target state)
###

kubectl delete deployment first-app
```

### Docker Hub - create a new repository
- repository name : kub-first-app

docker tag
```
docker tag kub-first-app ralf418/kub-first-app
docker push ralf418/kub-first-app
```

### recreate kube image
```
kubectl create deployment first-app --image=ralf418/kub-first-app
kubectl get deployment
kubectl get pods
```

### Create a network accessible from outside
```
# kubectl expose
# --port=8080
# --type=
### Loadbalancer / NodePort / ClusterIP
kubectl expose deployment first-app --type=LoadBalancer --port=8080
kubectl get services
### NAME         TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)          AGE
### first-app    LoadBalancer   10.xxx.xxx.xxx <pending>     8080:32675/TCP   25s
### kubernetes   ClusterIP      10.xxx.xxx.xxx        <none>        443/TCP          178m

## minikube network connect
minikube service first-app
```

### Autoscale
```
kubectl scale deployment/first-app --replicas=3
kubectl get pods
kubectl scale deployment/first-app --replicas=1
```

### Update deployment
```
### updated source
docker build -t ralf418/kub-first-app .
docker push ralf418/kub-first-app
kubectl set image deployment/first-app kub-first-app=ralf418/kub-first-app
kubectl get deployment
### not update
### tag version
docker build -t ralf418/kub-first-app:2 .
docker push ralf418/kub-first-app:2
kubectl set image deployment/first-app kub-first-app=ralf418/kub-first-app:2
kubectl get deployment
kubectl rollout status deployment/first-app
```

### deployment rollback
```
### update missing image
kubectl set image deployment/first-app kub-first-app=ralf418/kub-first-app:3
kubectl rollout status deployment/first-app
# error but no problem web access
kubectl get pods
kubectl rollout undo deployment/first-app
kubectl get pods
```

### deployment history and rollback to an earlier time
```
kubectl rollout history deployment/first-app
kubectl rollout history deployment/first-app --revision=1

kubectl rollout undo deployment/first-app --to-revision=1
```

### delete service & deployment
```
kubectl delete service first-app
kubectl delete deployment first-app
```
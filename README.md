# Ruby on Rails Application
 Here is a description on how to transform rails app from docker into k8s 
## prepare docker image

create rail-app docker image and push it to a docker hub repo

```bash
docker-compose build
docker tag drkiq mohamedkhaled-incorta/rails-app:latest
docker push mohamedkhaled-incorta/rails-app:latest
```
# Kubernetes
## PersistentVoulumes 

```bash
kubectl create -f kube-files/kube-volumes.yml
```

## Postgres database
Deploy postgres database
```bash
kubectl create -f kube-files/dep-files/postgres-dep.yml
kubectl create -f kube-files/svc-files/postgres-svc.yml
```

## Redis 
Deploy Redis App
```bash
kubectl create -f kube-files/dep-files/redis-dep.yml
kubectl create -f kube-files/svc-files/redis-svc.yml
```
## Intialize Postgres DB

```bash
kubectl create -f kube-files/setup.yml
```
## Drkiq
Deploy Drkiq App
```bash
kubectl create -f kube-files/dep-files/drkiq-dep.yml
kubectl create -f kube-files/svc-files/drkiq-svc.yml
```
## Sidekiq
```bash
kubectl create -f kube-files/svc-files/sidekiq-dep.yml
```
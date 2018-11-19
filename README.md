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
kubectl create -f kube-files/jobs/db-intialize.yml
```
## Drkiq
Deploy Drkiq App
```bash
kubectl create -f kube-files/dep-files/drkiq-dep.yml
kubectl create -f kube-files/svc-files/drkiq-svc.yml
```
## Sidekiq
```bash
kubectl create -f kube-files/dep-files/sidekiq-dep.yml
```

## Submit controller job 
```bash
kubectl create -f kube-files/jobs/controller-job.yml
```

## Expose drkiq Deployment to external IP using LB   
```bash
kubectl create -f kube-files/svc-files/rail-lb.yml
```

## Create ConfigMaps   
```bash
kubectl create configmap rails-configmap --from-env-file=kube-files-configmaps/rail-configmap.yml
```

## Deploy using configmaps 
```bash
kubectl create -f kube-files-configmaps/kube-volumes.yml
kubectl create configmap rails-configmap --from-env-file=kube-files-configmaps/rail-configmap.yml
kubectl create -f kube-files-configmaps/dep-files/postgres-dep.yml
kubectl create -f kube-files-configmaps/svc-files/postgres-svc.yml
kubectl create -f kube-files-configmaps/svc-files/redis-svc.yml
kubectl create -f kube-files-configmaps/dep-files/redis-dep.yml
kubectl create -f kube-files-configmaps/jobs/db-intialize.yml
kubectl create -f kube-files-configmaps/dep-files/drkiq-dep.yml
kubectl create -f kube-files-configmaps/svc-files/drkiq-svc.yml
kubectl create -f kube-files-configmaps/dep-files/sidekiq-dep.yml
kubectl create -f kube-files-configmaps/jobs/controller-job.yml
```  
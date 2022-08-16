a real example: robotshop
-------------------------
```
git submodule add git@github.com:linuxacademy/robot-shop.git
```

!!! robot-shop is outdated !!!  
apply robotshop-k8s-update.diff



for a larger app - good idea to create a namespace
```
kubectl create namespace robot-shop
kubectl get namespaces
```

execute all descriptors
```
kubectl -n robot-shop create -f ./robot-shop/K8s/descriptors/

curl host.docker.internal:30080
```

change running microservice on-the-fly
```

```
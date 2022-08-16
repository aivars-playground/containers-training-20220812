efectively - a load balancer on top ff nodes

```
kubectl create -f nginx-simple-service.yaml

kubectl get services
> NAME           TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
> kubernetes     ClusterIP   10.96.0.1     <none>        443/TCP        21h
> ngix-service   NodePort    10.99.75.21   <none>        80:30080/TCP   3m14s

curl host.docker.internal:30080
> Welcome to nginx!
```


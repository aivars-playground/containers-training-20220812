deployments manage replicas
```
kubectl get deployments

> NAME    READY   UP-TO-DATE   AVAILABLE   AGE
> nginx   2/2     2            2           57m


kubectl describe deployment nginx
> ...
```


```
kubectl get pods

> NAME                     READY   STATUS    RESTARTS      AGE
> busybox                  1/1     Running   2 (20s ago)   33m
> nginx-5f57f89748-lz4rm   1/1     Running   0             61m
> nginx-5f57f89748-n87qq   1/1     Running   0             61m

kubectl delete pod nginx-5f57f89748-lz4rm

kubectl get pods
> NAME                     READY   STATUS              RESTARTS      AGE
> busybox                  1/1     Running             2 (80s ago)   34m
> nginx-5f57f89748-n87qq   1/1     Running             0             62m
> nginx-5f57f89748-tdvdw   0/1     ContainerCreating   0             2s
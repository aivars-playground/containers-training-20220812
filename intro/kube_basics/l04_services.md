efectively - a load balancer on top ff nodes

```
kubectl create -f nginx-simple-service.yaml

kubectl get services
> NAME           TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
> kubernetes     ClusterIP   10.96.0.1     <none>        443/TCP        21h
> ngix-service   NodePort    10.99.75.21   <none>        80:30080/TCP   3m14s

curl localhost:30080                    windows
curl host.docker.internal:30080         in docker
> Welcome to nginx!

kubectl exec busybox -- curl docker-desktop:30080   inside pod, access node by dns
kubectl exec busybox -- curl ngix-service:80        inside pod, access service by dns
kubectl exec busybox -- curl 10.99.75.21:80         inside pod, access service by ip
```
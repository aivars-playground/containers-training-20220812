POD kind
--------
```
kubectl create -f nginx-simple-pod.yaml

kubectl get pods
> NAME    READY   STATUS    RESTARTS   AGE
> nginx   1/1     Running   0          31s

kubectl describe pod nginx 

kubectl delete pod nginx

kubectl describe node docker-desktop
```

Deployment kind
---------------
```
ubectl create -f nginx-simple-deployment.yaml

kubectl get pods
NAME                     READY   STATUS    RESTARTS   AGE
nginx-5f57f89748-lz4rm   1/1     Running   0          91s
nginx-5f57f89748-n87qq   1/1     Running   0          91s
```

Schedule (deploy) without file
------------------------------
```
cat << EOF | kubectl create -f -
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  labels:
    name: busybox
spec:
  containers:
  - name: busybox
    image: radial/busyboxplus:curl
    args:
    - sleep
    - "1000"
EOF
```

```
kubectl exec busybox -- curl <ip_of_another_pod>

i.e.

kubectl exec busybox -- curl 10.1.0.15
```

Achitecture
-----------
```
#see all system pods
kubectl get pods -n kube-system
```
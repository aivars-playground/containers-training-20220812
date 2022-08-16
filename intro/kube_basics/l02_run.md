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
control plane
```
> kubectl get pods -n kube-system

etcd                    - provides distributed data store
kube-apiserver          - rest based api (kubextl is usong api)
kube-controller-manager - backend stuff controlling the cluster

> sudo systemctl status kubelet
kubelet -  The Kubernetes Node Agent: system service that controlls the cluster 

kube_proxy  - trafic routing rules
flannel     - network between nodes (other alternatives exist)
```
```
$ kubectl get nodes
NAME             STATUS   ROLES           AGE     VERSION
docker-desktop   Ready    control-plane   6m27s   v1.24.2
```

```
$ kubectl get pods --all-namespaces
kube-system   coredns-6d4b75cb6d-fh5l4                 1/1     Running   0             19m
kube-system   coredns-6d4b75cb6d-vjf5t                 1/1     Running   0             19m
  ...
kube-system   vpnkit-controller                        1/1     Running   1 (57s ago)   18m
```

```
$ kubectl create namespace pod-example
$ kubectl get namespaces
NAME              STATUS   AGE
default           Active   21m
kube-node-lease   Active   21m
kube-public       Active   21m
kube-system       Active   21m
pod-example       Active   19s
```

```
create and run pod
kubectl create -f .\pod-sample.yaml
kubectl delete namespace pod-example
```

```
> get pods -o wide
PS C:\Users\aivars.smaukstelis\kube_project> kubectl --namespace pod-example get pods -o wide
NAME         READY   STATUS    RESTARTS   AGE   IP         NODE             NOMINATED NODE   READINESS GATES
examplepod   2/2     Running   0          16m   10.1.0.6   docker-desktop   <none>           <none>
```

```
> curl 10.1.0.6:80
Mon Aug 15 14:24:29 UTC 2022
Mon Aug 15 14:26:09 UTC 2022
...
```





```yaml
# pod-sample.yaml
apiVersion: v1
kind: Pod
metadata:
  name: examplepod
  namespace: pod-example
spec:
  volumes:
    - name: html
      emptyDir: {}
  containers:
  - name: webcontainer
    image: nginx
    volumeMounts:
      - mountPath: /usr/share/nginx/html
        name: html
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
  - name: filecontainer
    image: debian
    volumeMounts:
      - mountPath: /html
        name: html
    command: ["/bin/sh", "-c"]
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
    args:
      - while true; do
          date >> /html/index.html;
          sleep 1;
        done
```

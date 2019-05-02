### Deploy nfs server pod and service
```
$ kubectl apply -f nfs-server.yaml
```

### Create text file in nfs server pod
```
$ kubectl exec -it nfs-server-pod sh
# echo 'Hello from Kubernetes storage' > /exports/index.txt
# exit
```

### Update persistent volume definition with nfs server ip address
```
$ kubectl get service nfs-service
```
Copy ClusterIP to nfs-pv.yaml's nfs.server field

### Create NFS persistent volume
```
$ kubectl apply -f nfs-pv.yaml
```

### Create NFS persistent volume claim
```
$ kubectl apply -f nfs-pvc.yaml
```

### Deploy pod with nfs persistent volume mounted to the container and see it have access to file
```
$ kubectl apply -f pod-node.yaml
```

### Check logs to see file from nfs being read and printed in a loop through node.js script
```
$ kubectl logs pod-using-nfs
Hello from Kubernetes storage

Hello from Kubernetes storage

Hello from Kubernetes storage
```

## References
https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-volumes-example-nfs-persistent-volume.html

https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/

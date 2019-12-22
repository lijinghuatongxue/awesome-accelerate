曲线救国策略

别整什么 github 和docker hub auto build，麻烦



`pull.sh`

```
#!/bin/bash
images=(
kube-proxy-amd64:v1.9.0 
kube-scheduler-amd64:v1.9.0 
kube-controller-manager-amd64:v1.9.0 
kube-apiserver-amd64:v1.9.0
etcd-amd64:3.1.10 
pause-amd64:3.0 
kubernetes-dashboard-amd64:v1.8.3 
k8s-dns-sidecar-amd64:1.14.7 
k8s-dns-kube-dns-amd64:1.14.7
k8s-dns-dnsmasq-nanny-amd64:1.14.7
)
for image in ${images[@]} ; do
  docker pull mirrorgooglecontainers/$image
  docker tag mirrorgooglecontainers/$image gcr.io/google_containers/$image
  docker rmi mirrorgooglecontainers/$image
done
```

```
$ bash pull.sh
```


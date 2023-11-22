# Get everything in every namespace
```
kubectl get all -A 


$ kubectl get all -A
NAMESPACE                         NAME                                           READY   STATUS    RESTARTS   AGE
cattle-fleet-local-system         pod/fleet-agent-545c88bf5f-kdjw5               1/1     Running   0          129m
cattle-fleet-system               pod/fleet-controller-77dc8fc97c-m8kgx          1/1     Running   0          156m
cattle-fleet-system               pod/gitjob-6dcbcd6ff5-q57bv                    1/1     Running   0          156m
cattle-provisioning-capi-system   pod/capi-controller-manager-7bc5589765-jmwzk   1/1     Running   0          154m
cattle-system                     pod/rancher-webhook-c9bd5c87c-j4nlz            1/1     Running   0          155m
kube-system                       pod/coredns-59b4f5bbd5-vtcrh                   1/1     Running   0          159m

NAMESPACE                         NAME                           TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                  AGE
cattle-fleet-system               service/gitjob                 ClusterIP   10.43.42.155    <none>        80/TCP                   156m
cattle-provisioning-capi-system   service/capi-webhook-service   ClusterIP   10.43.185.149   <none>        443/TCP                  154m
cattle-system                     service/rancher                ClusterIP   10.43.93.194    <none>        443/TCP                  160m
cattle-system                     service/rancher-webhook        ClusterIP   10.43.185.245   <none>        443/TCP                  155m
default                           service/kubernetes             ClusterIP   10.43.0.1       <none>        443/TCP                  160m
kube-system                       service/kube-dns               ClusterIP   10.43.0.10      <none>        53/UDP,53/TCP,9153/TCP   160m

NAMESPACE                         NAME                                      READY   UP-TO-DATE   AVAILABLE   AGE
cattle-fleet-local-system         deployment.apps/fleet-agent               1/1     1            1           129m
cattle-fleet-system               deployment.apps/fleet-controller          1/1     1            1           156m
cattle-fleet-system               deployment.apps/gitjob                    1/1     1            1           156m
cattle-provisioning-capi-system   deployment.apps/capi-controller-manager   1/1     1            1           154m
cattle-system                     deployment.apps/rancher-webhook           1/1     1            1           155m
kube-system                       deployment.apps/coredns                   1/1     1            1           160m

NAMESPACE                         NAME                                                 DESIRED   CURRENT   READY   AGE
cattle-fleet-local-system         replicaset.apps/fleet-agent-545c88bf5f               1         1         1       129m
cattle-fleet-system               replicaset.apps/fleet-controller-77dc8fc97c          1         1         1       156m
cattle-fleet-system               replicaset.apps/gitjob-6dcbcd6ff5                    1         1         1       156m
cattle-provisioning-capi-system   replicaset.apps/capi-controller-manager-7bc5589765   1         1         1       154m
cattle-system                     replicaset.apps/rancher-webhook-c9bd5c87c            1         1         1       155m
kube-system                       replicaset.apps/coredns-59b4f5bbd5                   1         1         1       159m

```

# Kubectl Version
```
kubectl version 
```

# Cluster Info
```
kubectl cluster-info


$ kubectl cluster-info 
Kubernetes control plane is running at https://localhost/k8s/clusters/local
CoreDNS is running at https://localhost/k8s/clusters/local/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

To further debug and diagnose cluster problems, use 'kubectl cluster-info dump'.

```


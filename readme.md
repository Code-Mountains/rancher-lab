# Setup Kubectl
```
sudo apt-get update

# apt-transport-https may be a dummy package; if so, you can skip that package
sudo apt-get install -y apt-transport-https ca-certificates curl

curl -fsSL https://pkgs.k8s.io/core:/stable:/v1.28/deb/Release.key | sudo gpg --dearmor -o /etc/apt/keyrings/kubernetes-apt-keyring.gpg

# This overwrites any existing configuration in /etc/apt/sources.list.d/kubernetes.list
echo 'deb [signed-by=/etc/apt/keyrings/kubernetes-apt-keyring.gpg] https://pkgs.k8s.io/core:/stable:/v1.28/deb/ /' | sudo tee /etc/apt/sources.list.d/kubernetes.list


sudo apt-get update

sudo apt-get install -y kubectl

$ kubectl version --client

Client Version: v1.28.4
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3

```

# Rancher Setup 
```
sudo docker run --privileged -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher


## OUTPUT: 

$ docker ps -a 
CONTAINER ID   IMAGE             COMMAND           CREATED          STATUS          PORTS                                                                      NAMES
e371fd9da8ef   rancher/rancher   "entrypoint.sh"   43 seconds ago   Up 42 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp, 0.0.0.0:443->443/tcp, :::443->443/tcp   great_wing
f34f878075f7   rancher/rancher   "entrypoint.sh"   44 minutes ago   Created                                                                                    magical_lamarr
```

# Retrieve Rancher Password
```
$ docker logs e371fd9da8ef 2>&1 | grep "Bootstrap Password:"

2023/11/21 23:12:30 [INFO] Bootstrap Password: nkkvl9h5hhwnpjlk4dlf6xfctwvc7xs7dxdbc5b46ktzlkc6mskkd9
```

# Rancher First Time Setup
```
 Howdy!

Welcome to Rancher

It looks like this is your first time visiting Rancher; if you pre-set your own bootstrap password, enter it here. Otherwise a random one has been generated for you. To find it:

For a "docker run" installation:

    Find your container ID with docker ps, then run:
    docker logs container-id 2>&1 | grep "Bootstrap Password:" 


For a Helm installation, run:

kubectl get secret --namespace cattle-system bootstrap-secret -o go-template='{{.data.bootstrapPassword|base64decode}}{{"\n"}}'
Password
Show
English

```

# Run Rancher with Helm
```
helm upgrade --install rancher rancher/rancher --namespace cattle-system --create-namespace \
--set hostname=rancher.$INGRESS_HOST.nip.io \
--set bootstrapPassword=admin \
--set ingress.tls.source=letsEncrypt \
--set letsEncrypt.email=$LE_EMAIL \
--wait
```


# Reset Rancher Password from Docker:
```
$ docker exec -it e371fd9d reset-password
New password for default admin user (user-2wfsq):
zocauNX2jbT3s7eawRkE
```

# Deploy a NodeJS App on Kubernetes and Rancher
```
https://www.suse.com/c/rancher_blog/deploy-a-nodejs-app-on-kubernetes-and-rancher/
```

# Building a NodeJS Application using MongoDB and Rancher – Part 1
```
https://www.suse.com/c/rancher_blog/building-a-nodejs-application-using-mongodb-and-rancher-part-1/
```

# Build a NodeJS App using MongoDB and Rancher - part 2
```
https://www.rancher.cn/nodejs-mongodb-application-with-rancher-part-2
```

# Installing Helm:
```
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm


$ helm version
WARNING: Kubernetes configuration file is group-readable. This is insecure. Location: /home/sysadmin/.kube/config
WARNING: Kubernetes configuration file is world-readable. This is insecure. Location: /home/sysadmin/.kube/config
version.BuildInfo{Version:"v3.13.2", GitCommit:"2a2fb3b98829f1e0be6fb18af2f6599e0f4e8243", GitTreeState:"clean", GoVersion:"go1.20.10"}
```


# Install K3s on Linux: 
```
$ curl -sfL https://get.k3s.io | sh -s - server --cluster-init
[INFO]  Finding release for channel stable
[INFO]  Using v1.27.7+k3s2 as release
[INFO]  Downloading hash https://github.com/k3s-io/k3s/releases/download/v1.27.7+k3s2/sha256sum-amd64.txt
[INFO]  Downloading binary https://github.com/k3s-io/k3s/releases/download/v1.27.7+k3s2/k3s
[INFO]  Verifying binary download
[INFO]  Installing k3s to /usr/local/bin/k3s
[INFO]  Skipping installation of SELinux RPM
[INFO]  Skipping /usr/local/bin/kubectl symlink to k3s, command exists in PATH at /usr/bin/kubectl
[INFO]  Creating /usr/local/bin/crictl symlink to k3s
[INFO]  Skipping /usr/local/bin/ctr symlink to k3s, command exists in PATH at /usr/bin/ctr
[INFO]  Creating killall script /usr/local/bin/k3s-killall.sh
[INFO]  Creating uninstall script /usr/local/bin/k3s-uninstall.sh
[INFO]  env: Creating environment file /etc/systemd/system/k3s.service.env
[INFO]  systemd: Creating service file /etc/systemd/system/k3s.service
[INFO]  systemd: Enabling k3s unit
Created symlink /etc/systemd/system/multi-user.target.wants/k3s.service → /etc/systemd/system/k3s.service.
[INFO]  systemd: Starting k3s


$ sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
$ sudo chown -R sysdamin:sysadmin ~/.kube/
$ sudo chown -R sysadmin:sysadmin ~/.kube/

$ kubectl get all -A
NAMESPACE     NAME                                         READY   STATUS      RESTARTS   AGE
kube-system   pod/coredns-77ccd57875-pz6f6                 1/1     Running     0          106s
kube-system   pod/helm-install-traefik-crd-ggktb           0/1     Completed   0          106s
kube-system   pod/helm-install-traefik-qfktc               0/1     Completed   1          106s
kube-system   pod/local-path-provisioner-957fdf8bc-5hcdk   1/1     Running     0          106s
kube-system   pod/metrics-server-648b5df564-s2t9h          1/1     Running     0          106s
kube-system   pod/svclb-traefik-c38b53c0-c5tpw             2/2     Running     0          90s
kube-system   pod/traefik-768bdcdcdd-68cqt                 1/1     Running     0          90s

NAMESPACE     NAME                     TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)                      AGE
default       service/kubernetes       ClusterIP      10.43.0.1      <none>         443/TCP                      2m2s
kube-system   service/kube-dns         ClusterIP      10.43.0.10     <none>         53/UDP,53/TCP,9153/TCP       118s
kube-system   service/metrics-server   ClusterIP      10.43.62.39    <none>         443/TCP                      117s
kube-system   service/traefik          LoadBalancer   10.43.25.123   192.168.0.20   80:31545/TCP,443:31759/TCP   90s

NAMESPACE     NAME                                    DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
kube-system   daemonset.apps/svclb-traefik-c38b53c0   1         1         1       1            1           <none>          90s

NAMESPACE     NAME                                     READY   UP-TO-DATE   AVAILABLE   AGE
kube-system   deployment.apps/coredns                  1/1     1            1           118s
kube-system   deployment.apps/local-path-provisioner   1/1     1            1           118s
kube-system   deployment.apps/metrics-server           1/1     1            1           117s
kube-system   deployment.apps/traefik                  1/1     1            1           90s

NAMESPACE     NAME                                               DESIRED   CURRENT   READY   AGE
kube-system   replicaset.apps/coredns-77ccd57875                 1         1         1       106s
kube-system   replicaset.apps/local-path-provisioner-957fdf8bc   1         1         1       106s
kube-system   replicaset.apps/metrics-server-648b5df564          1         1         1       106s
kube-system   replicaset.apps/traefik-768bdcdcdd                 1         1         1       90s

NAMESPACE     NAME                                 COMPLETIONS   DURATION   AGE
kube-system   job.batch/helm-install-traefik       1/1           18s        116s
kube-system   job.batch/helm-install-traefik-crd   1/1           16s        116s


```
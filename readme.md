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
--set ingress.tls.source=letsEncrypt
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
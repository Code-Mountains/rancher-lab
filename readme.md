# Rancher Setup 
```
sudo docker run --privileged -d --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher


## OUTPUT: 

$ docker ps -a 
CONTAINER ID   IMAGE             COMMAND           CREATED          STATUS          PORTS                                                                      NAMES
e371fd9da8ef   rancher/rancher   "entrypoint.sh"   43 seconds ago   Up 42 seconds   0.0.0.0:80->80/tcp, :::80->80/tcp, 0.0.0.0:443->443/tcp, :::443->443/tcp   great_wing
f34f878075f7   rancher/rancher   "entrypoint.sh"   44 minutes ago   Created                                                                                    magical_lamarr


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
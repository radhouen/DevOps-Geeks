In this lesson we will be installing Istio in a Docker environment. We will take a quick look at the moving parts and how they work together, as well as installing an application and ensuring the everything is working as expected. Although we are covering installation into a Docker environment, this is not as feature rich as some other installations. This is included here because it is officially documented and there is some talk of more features being added in the future.

Commands used in this lesson:
Add current user to docker group

```properties
sudo usermod -aG docker cloud_user
```

Install docker-compose and make it executable

```properties
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-Linux-x86_64" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose
```

Download Istio and unpack it

```properties
wget https://github.com/istio/istio/releases/download/1.0.6/istio-1.0.6-linux.tar.gz

tar -xvf istio-1.0.6-linux.tar.gz
```

Preconfigure kubectl for pilot

```properties
kubectl config set-context istio --cluster=istio
kubectl config set-cluster istio --server=http://localhost:8080
kubectl config use-context istio
```


Create a DOCKER_GATEWAY environment variable
```properties
export DOCKER_GATEWAY=172.28.0.1:
```
Bring up Istio's control plane

Remember: this may need to be repeated to ensure the pilot container starts:

```properties
docker-compose -f install/consul/istio.yaml up -d
```

Change bookinfo.yaml to set port 30080 in place of port 9081

```properties
sed -i 's/9081/30080/' ./istio-1.0.6/samples/bookinfo/platform/consul/bookinfo.yaml
`
```
Bring up the application


```properties
docker-compose -f ./istio-1.0.6/samples/bookinfo/platform/consul/bookinfo.yaml up -d
```
Bring up the sidecars

```properties
docker-compose -f ./istio-1.0.6/samples/bookinfo/platform/consul/bookinfo.sidecars.yaml up -d
```
How do you feel about this video?

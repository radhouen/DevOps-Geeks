### Imperative vs Declaritive approaches
There’s generally two ways to use kubectl when managing your kubernetes objects (pods, services,…etc), they are the Declaritive and Imperative approaches.

The Declaritive approach is about using the kubectl apply command when creating objects. That’s the approach we took in our hello-world demo. The declarative approach therefore depends on us first creating the yaml files before we can create the objects.

The imperative approach involves using any of the verb based commands, here are some them:

* kubectl run
* kubectl create
* kubectl expose
* kubectl delete
* kubectl edit

For example to imperitavely create our pod we would use the kubectl run command:

```yaml
kubectl run pod-httpd --image=httpd --labels="app=apache_webserver" --restart=Never

kubectl run pod-httpd --image=httpd --restart=Never --dry-run -o yaml > pod.yaml

kubectl create service nodeport svc-nodeport-httpd --node-port=31000 --tcp=3050:80 > service.yaml
```

```yml
kubectl run --generator=run-pod/v1 nginx-pod --image=nginx:alpine
```


```yaml
kubectl run --generator=run-pod/v1 redis --image=redis:alpine --dry-run -o yaml>redis-pod.yml
```
1. Outout

#### add labels tier=db

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: redis
    tier: db
  name: redis
spec:
  containers:  - image: redis:alpine
    name: redis    resources: {}
  dnsPolicy: ClusterFirst
  restartPolicy: Always
status: {}
```


### Create a service for redis type clusterIp and expose port 6379:

```yaml
kubectl expose pod redis --port=6379 --name redis-service
```



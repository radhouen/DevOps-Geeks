Developement | Default  | Production
------------ | ------------- | -------------
kubectl get pods --namespace=dev | kubectlget pods | kubectl get pods --namespace=prod


```yaml
kubectl config set-context $(kubectl config current-context) --namespace=dev
```

```yaml
kubectl get pods --namespace=default
```

```yaml
kubectl get pods --all-namespaces
```


### Limit ressources for a namespace:

```yaml
apiVersion: v1
kind: ResourceQuota
metadata:
  name: compute-quota
  namespace: dev
spec:
  hard:
    pods: "10"
    requests.cpu: "4"
    request.memory: 5Gi
    limits.cpu: "10"
    limits.memory: 10Gi
```
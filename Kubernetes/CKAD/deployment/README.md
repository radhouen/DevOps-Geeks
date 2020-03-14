rollout :deploy new version (upgrade application == rolling update)
rollback : go back to last version



# Certification Tip: Imperative Commands
Here's a tip!



As you might have seen already, it is a bit difficult to create and edit YAML files. Especially in the CLI. During the exam, you might find it difficult to copy and paste YAML files from browser to terminal. Using the kubectl run command can help in generating a YAML template. And sometimes, you can even get away with just the kubectl run command without having to create a YAML file at all. For example, if you were asked to create a pod or deployment with specific name and image you can simply run the kubectl run command.

Use the below set of commands and try the previous practice tests again, but this time try to use the below commands instead of YAML files. Try to use these as much as you can going forward in all exercises

Reference (Bookmark this page for exam. It will be very handy):

https://kubernetes.io/docs/reference/kubectl/conventions/



### Create an NGINX Pod
```yaml
kubectl run --generator=run-pod/v1 nginx --image=nginx
```


Generate POD Manifest YAML file (-o yaml). Don't create it(--dry-run)
```yaml
kubectl run --generator=run-pod/v1 nginx --image=nginx --dry-run -o yaml
```



### Create a deployment

```yaml
kubectl create deployment --image=nginx nginx
```


Generate Deployment YAML file (-o yaml). Don't create it(--dry-run)

```yaml
kubectl create deployment --image=nginx nginx --dry-run -o yaml
```


Generate Deployment YAML file (-o yaml). Don't create it(--dry-run) with 4 Replicas (--replicas=4)

```yaml
kubectl create deployment --image=nginx nginx --dry-run -o yaml > nginx-deployment.yaml
```
Save it to a file, make necessary changes to the file (for example, adding more replicas) and then create the deployment.


---

# Certification Tip: Formatting Output with kubectl


The default output format for all kubectl commands is the human-readable plain-text format.

The -o flag allows us to output the details in several different formats.


```yaml
kubectl [command] [TYPE] [NAME] -o <output_format>
```
Here are some of the commonly used formats:



1. -o jsonOutput a JSON formatted API object.

2. -o namePrint only the resource name and nothing else.

3. -o wideOutput in the plain-text format with any additional information.

4. -o yamlOutput a YAML formatted API object.

Here are some useful examples:

## Output with JSON format:
```yaml
master $ kubectl create namespace test-123 --dry-run -o json
```

```json
{
    "kind": "Namespace",
    "apiVersion": "v1",
    "metadata": {
        "name": "test-123",
        "creationTimestamp": null
    },
    "spec": {},
    "status": {}
}
```

## Output with YAML format:
```yaml
master $ kubectl create namespace test-123 --dry-run -o yaml
```

```yaml
apiVersion: v1
kind: Namespace
metadata:
  creationTimestamp: null
  name: test-123
spec: {}
status: {}
```

Output with wide (additional details):

Probably the most common format used to print additional details about the object:

```yaml
master $ kubectl get pods -o wide
NAME      READY   STATUS    RESTARTS   AGE     IP          NODE     NOMINATED NODE   READINESS GATES
busybox   1/1     Running   0          3m39s   10.36.0.2   node01   <none>           <none>
ningx     1/1     Running   0          7m32s   10.44.0.1   node03   <none>           <none>
redis     1/1     Running   0          3m59s   10.36.0.1   node01   <none>           <none>
master $
```

For more details, refer:

https://kubernetes.io/docs/reference/kubectl/overview/

https://kubernetes.io/docs/reference/kubectl/cheatsheet/
Learning Objectives
check_circle
Search for, Download, and Decompress a Copy of the Most Recent Wordpress Chart from the `stable` Repository
keyboard_arrow_up

On the Kubernetes master server issue the command:

```yaml
[cloud_user@km]$ helm search wordpress
```

In the output of this command locate the stable/wordpress chart.

Download and uncompress local copy of this chart using the command:

```yaml
[cloud_user@km]$ helm fetch --untar stable/wordpress
```
Confirm that you have a directory named wordpress:

```yaml
[cloud_user@km]$ ls -l
```

This should show a wordpress directory.
check_circle
Modify the Chart to Allow It to Run without Persistence, and Set the Service to Run as 'NodePort' with an HTTP port of `30080`
keyboard_arrow_up

Locate the values.yaml file in the wordpress directory and open it in an editor (we're using Vim here):

```yaml
[cloud_user@km]$ cd ./wordpress
[cloud_user@km]$ ls
[cloud_user@km]$ vim values.yaml
```

Locate the 2 locations that contain the persistence setting:
```yaml
persistence:
  enabled: true

Set these values to:

persistence:
  enabled: false
```
There will be one for the MariaDB and one for the Wordpress installation.
Locate the Service definition and set it to:
```yaml
service:
    type: NodePort
    port: 80
    httpsPort: 443
    nodePorts:
      http: "30080"
      https: ""
```
Once this is complete save and quit.
check_circle
Install the Wordpress Chart and Verify That It Is Working
keyboard_arrow_up

From the home directory, run the install command for the chart:
```yaml
[cloud_user@km]$ cd ~
[cloud_user@km]$ helm install ./wordpress
```
In the output of this command, confirm that the service is set to NodePort.

Once this is done, wait for the pods to become ready using:

```yaml
[cloud_user@km]$ kubectl get pods
```
Ignore the busybox line. Run this command every so often until we get 1/1 as a READY status. When they are ready, copy the public IP address of kn1. Open a browser and navigate to:

```yaml
http://<kn1_IP_address>:30080
```
Confirm that the wordpress application is up and running.
check_circle
Clean up the Kubernetes Cluster and Ensure That There Are No Artifacts
keyboard_arrow_up

Get the release name for the Wordpress release:

```yaml
[cloud_user@km]$ helm ls --short
```
Remove the helm release:

```yaml
[cloud_user@km]$ helm delete <RELEASE_NAME>
```
Confirm that there are no deployed resources. None of these commands (except for get pods, but we're ignoring busybox anyway, remember?) should return information:

```yaml
[cloud_user@km]$ helm ls
[cloud_user@km]$ kubectl get pods
[cloud_user@km]$ kubectl get pv
[cloud_user@km]$ kubectl get pvc
```

Related Courses
Helm Deep Dive
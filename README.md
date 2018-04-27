# kube-dash

Runs a dash full node in a kubernetes cluster.


## Prerequisites

First provision a disk:

```console
gcloud compute disks create --size=20GB dash-data
```

Next create a secret file from the template:

```console
cp deploy/dash-secret.yml.template deploy/dash-secret.yml
```

Then find the base64 encoding of the username and password you want to use:

```console
echo -n YOURUSERNAME | base64
echo -n YOURPASSWORD | base64
```

Fill in those values in the `dash-secret.yml` file.

Finally create the kubernetes resources:

```console
kubectl create -f deploy/
```


### Debugging

If your dash node is crashing but you need to ssh in and look at the disk
contents, deploy the debug pod (a recent version of Ubuntu, for convenience):

```console
kubectl create -f debug/
```

Now you can ssh into the debug pod:

```console
kubectl exec -it dash-debug -- /bin/bash
ls -lhtra /data
```

Make sure to tear down the pod when you're done:

```console
kubectl delete -f debug/
```

### Other useful commands

Cluster creation (Create cluster on web):

```console
gcloud container clusters create dash-cluster  --zone=us-central1-c
```

Get pods (Workloads on web):
```console
kubectl get pods
```

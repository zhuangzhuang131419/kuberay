# Ray Cluster

Make sure ray-operator has been deployed.

[Ray](https://ray.io/) is An open source framework that provides a simple, universal API for building distributed applications. Ray is packaged with RLlib, a scalable reinforcement learning library, and Tune, a scalable hyperparameter tuning library.

## Helm

```console
$ helm version
version.BuildInfo{Version:"v3.6.2", GitCommit:"ee407bdf364942bcb8e8c665f82e15aa28009b71", GitTreeState:"dirty", GoVersion:"go1.16.5"}
```

## TL;DR;

```console
helm install --name ray-cluster-helm . --values values.yaml --namespace default
```

## Installing the Chart

To install the chart with the release name `my-release`:


```console
helm install --name sample ray-cluster-helm --values ray-cluster-helm/values.yaml --namespace default
```

> note: The chart will submit a RayCluster. 


## Uninstalling the Chart

To uninstall/delete the `my-release` deployment:

```console
helm delete ray-cluster-helm
```

The command removes nearly all the Kubernetes components associated with the
chart and deletes the release.

## Check Cluster status

### Get Service 

```console
$ kubectl get svc -l ray.io/cluster=ray-cluster-helm
NAME                       TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)                       AGE
ray-cluster-helm-head-svc   ClusterIP   10.103.36.68   <none>        10001/TCP,6379/TCP,8265/TCP   9m24s
```

## Forward to dashboard

```console
$ kubectl get pod -o wide
NAME                                       READY   STATUS    RESTARTS   AGE    IP            NODE             NOMINATED NODE   READINESS GATES
ray-cluster-helm-head-sd77l                 1/1     Running   0          8h     10.1.61.208   docker-desktop   <none>           <none>
ray-cluster-helm-worker-workergroup-czxd6   1/1     Running   0          8h     10.1.61.207   docker-desktop   <none>           <none>
ray-operator-helm-687785b964-jgfhv          1/1     Running   6          3d4h   10.1.61.196   docker-desktop   <none>           <none>

$ kubectl port-forward ray-cluster-helm-head-sd77l 8265
Forwarding from 127.0.0.1:8265 -> 8265
Forwarding from [::1]:8265 -> 8265
```
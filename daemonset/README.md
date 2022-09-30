# Daemonset

A DaemonSet ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them. As nodes are removed from the cluster, those Pods are garbage collected. Deleting a DaemonSet will clean up the Pods it created.

Some typical uses of a DaemonSet are:

1. To run a daemon for cluster storage on each node, such as: - glusterd - ceph
2. To run a daemon for logs collection on each node, such as: - fluentd - logstash
3. To run a daemon for node monitoring on ever note, such as: - Prometheus Node Exporter - collectd - Datadog agent



``` 
$ kubectl create -f daemonset.yml --record 
```

The --record flag will track changes made through each revision.

```
$ kubectl get daemonsets/prometheus-daemonset
```

```
kubectl describe daemonset/prometheus-daemonset
```

### Getting pods in daemonset:

``` 
$ kubectl get pods -lname=prometheus-exporter
```

### Delete a daemonset:

```
$ kubectl delete -f daemonset.yml
```


##  Restrict DaemonSets To Run On Specific Nodes

By default, a DaemonSet schedules its pods on all the cluster nodes. But sometimes you may need to run specific processes on specific nodes. For example, nodes that host database pods need different monitoring or logging rules. DaemonSets allow you to select which nodes you want to run the pods on. You can do this by using nodeSelector. With nodeSelector, you can select nodes by their labels the same way you do with pods. However, Kubernetes also allows you to select nodes based on some already-defined node properties. For example, kubernetes.io/hostname matches the node name. So, our example cluster has two nodes. We can modify the DaemonSet definition to run only on the first node. Lets’ first get the node names:

```
$kubectl get nodes
NAME    STATUS   ROLES    AGE   VERSION
node1   Ready    master   17m   v1.14.9
node2   Ready    <none>   17m   v1.14.9
```

You need to add the below entry in the above YAML file:

```
nodeSelector:
    	  kubernetes.io/hostname: node1
 ```

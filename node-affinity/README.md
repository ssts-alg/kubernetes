####
Node affinity is a set of rules used by the scheduler to determine where a pod can be placed. The rules are defined using custom labels on nodes and label selectors specified in pods. Node affinity allows a pod to specify an affinity (or anti-affinity) towards a group of nodes it can be placed on.
https://kubernetes.io/docs/tasks/configure-pod-container/assign-pods-nodes-using-node-affinity/


##### Add a label to a node

List the nodes in your cluster, along with their labels:

`kubectl get nodes --show-labels`

The output is similar to this:

```
NAME      STATUS    ROLES    AGE     VERSION        LABELS
worker0   Ready     <none>   1d      v1.13.0        ...,kubernetes.io/hostname=worker0
worker1   Ready     <none>   1d      v1.13.0        ...,kubernetes.io/hostname=worker1
worker2   Ready     <none>   1d      v1.13.0        ...,kubernetes.io/hostname=worker2
```

Choose one of your nodes, and add a label to it:

`kubectl label nodes <your-node-name> disktype=ssd`

where <your-node-name> is the name of your chosen node.

Verify that your chosen node has a disktype=ssd label:

`kubectl get nodes --show-labels`

The output is similar to this:
```
NAME      STATUS    ROLES    AGE     VERSION        LABELS
worker0   Ready     <none>   1d      v1.13.0        ...,disktype=ssd,kubernetes.io/hostname=worker0
worker1   Ready     <none>   1d      v1.13.0        ...,kubernetes.io/hostname=worker1
worker2   Ready     <none>   1d      v1.13.0        ...,kubernetes.io/hostname=worker2
```
In the preceding output, you can see that the worker0 node has a disktype=ssd label.

### Schedule a Pod using required node affinity

This manifest describes a Pod that has a requiredDuringSchedulingIgnoredDuringExecution node affinity,disktype: ssd. This means that the pod will get scheduled only on a node that has a disktype=ssd label.
pods/pod-nginx-required-affinity.yaml [Copy pods/pod-nginx-required-affinity.yaml to clipboard]

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: disktype
            operator: In
            values:
            - ssd            
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
```
Apply the manifest to create a Pod that is scheduled onto your chosen node:

`kubectl apply -f https://k8s.io/examples/pods/pod-nginx-required-affinity.yaml`

Verify that the pod is running on your chosen node:

`kubectl get pods --output=wide`

The output is similar to this:
```
NAME     READY     STATUS    RESTARTS   AGE    IP           NODE
nginx    1/1       Running   0          13s    10.200.0.4   worker0
```
### Schedule a Pod using preferred node affinity

This manifest describes a Pod that has a preferredDuringSchedulingIgnoredDuringExecution node affinity,disktype: ssd. This means that the pod will prefer a node that has a disktype=ssd label.
pods/pod-nginx-preferred-affinity.yaml [Copy pods/pod-nginx-preferred-affinity.yaml to clipboard]

```
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  affinity:
    nodeAffinity:
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 1
        preference:
          matchExpressions:
          - key: disktype
            operator: In
            values:
            - ssd          
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
```
Apply the manifest to create a Pod that is scheduled onto your chosen node:

`kubectl apply -f https://k8s.io/examples/pods/pod-nginx-preferred-affinity.yaml`

Verify that the pod is running on your chosen node:

`kubectl get pods --output=wide`

The output is similar to this:
```
NAME     READY     STATUS    RESTARTS   AGE    IP           NODE
nginx    1/1       Running   0          13s    10.200.0.4   worker0
```

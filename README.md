## Table of Contents:
1. Pods                 
2. ReplicaSet
3. ReplicationController
4. Deployments
5. Services
6. ConfigMap
7. Namespaces
8. HPA(Horizontal Pod Autoscaler)
9. Volumes
10. Secrets
11. Probes
12. NodeAffinity
13. EKSCTL(Cluster Creation)

# General Commands

## kubectl Cheat Sheet

[kubectl Cheat Sheet link](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)



#### Creating a replication controller with kubectl
`kubectl create deployment  apache --image=httpd --replicas=2 --port=80`
`kubectl create deployment myapp --image=sstechnosolutions/myapp:v0 ---replicas=5 -port=8080`

#### Expose containers
`kubectl expose deployment apache --port=80 --type=LoadBalancer`


#### Get labels of nodes
`kubectl get nodes --show-labels`



#### Get labels of pods
`kubectl get pods --show-labels`

#### To Run pod in perticular node

```
apiVersion: v1
kind: Pod
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  containers:
    - name: nodeapp
      image: sstechnosolutions/myapp:v0
      imagePullPolicy: Always
      ports:
        - containerPort: 8080
   nodeSelector:
      topology.kubernetes.io/zone: us-west-2a

```


#### To delete pods all at once

`kubectl delete pod --all`

#### To export config or To use different config
`export KUBECONFIG=~/.kube/config:/Users/admin/Desktop/dev_config`


#### Get Current namespace

```
kubectl config view | grep namespace
kubectl config view --minify -o jsonpath='{..namespace}' | xargs
```

#### Taints and Tolerations:

Node affinity is a property of Pods that attracts them to a set of nodes (either as a preference or a hard requirement). Taints are the opposite -- they allow a node to repel a set of pods. Tolerations are applied to pods. Tolerations allow the scheduler to schedule pods with matching taints.

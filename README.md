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

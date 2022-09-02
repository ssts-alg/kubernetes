# Kubernetes Pods - Commands

### Create pod by using command

```
$ kubectl run myapp --image=sstechnosolutions/myapp:v0 --port=8080
```

## Creating a Pod
### Create pod.yml with following content
Get the file [(pod.yml)](https://github.com/ssts-alg/kubernetes/blob/master/pods/pods.yml)
```
apiVersion: v1
kind: Pod
metadata:
  name: myapp
  labels:
    app: myapp
spec:
  containers:
    - name: myapp
      image: sstechnosolutions/myapp:v0
      imagePullPolicy: Always
      ports:
        - containerPort: 8080
```

```
$ kubectl create -f https://raw.githubusercontent.com/ssts-alg/kubernetes/master/pods/pods.yml
```
### Command to get all pods

```
$ kubectl get pods/po
```

### Command to describe pod details
**Syntax** - kubectl describe pods/POD_NAME

```
$ kubectl describe pods/myapp
```

### Executing commands on pods
**Syntax** - kubectl exec POD_NAME CMD_TO_EXECUTE
```
$ kubectl exec myapp printenv
$ kubectl exec myapp ls
```
### Getting into pods Terminal
**Syntax** - kubectl exec -it POD_NAME bash
```
$ kubectl exec -it myapp bash
```
### Get logs from pods
**Syntax** - kubectl logs POD_NAME
```
$ kubectl logs myapp
```
#####  Exposing Pods to Internet
By default Pods run in a isolated environment i.e. they are reachable within kubernetes cluster, if you wanna reach your pod outside cluster, You have to expose it
```
$ kubectl expose pods/myapp --type="NodePort" --port 8080
```







export KUBECONFIG=~/.kube/config:/Users/admin/Desktop/dev_config

# General Commands

#### Expose containers
`kubectl expose pods/myapp --type="NodePort" --port 8080`

#### Creating a replication controller with kubectl
`kubectl create deployment myapp --image=devopsmptech/myapp:2.0.12 ---replicas=5 -port=8080`

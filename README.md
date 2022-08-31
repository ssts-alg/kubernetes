# General Commands

#### Creating a replication controller with kubectl
`kubectl create deployment  apache --image=httpd --replicas=2 --port=80`
`kubectl create deployment myapp --image=sstechnosolutions/myapp:v0 ---replicas=5 -port=8080`

#### Expose containers
`kubectl expose deployment apache --port=80 --type=LoadBalancer`

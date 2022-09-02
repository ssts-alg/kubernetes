#### To Create Namespace form command line
`kubectl create namespace dev`

#### To Create Namespace form yaml file
`kubectl create -f namespaces/ns.yaml`

### Get all namespaces
`kubectl get namespaces/ns`

### Deleting a namespace
`kubectl delete namespaces dev`


### To set switch/default namespace
`kubectl config set-context --current --namespace=dev`

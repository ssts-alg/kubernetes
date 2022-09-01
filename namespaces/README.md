#### To Create Namespace form command line
`kubectl create namespace dev`

#### To Create Namespace form yaml file
`kubectl create -f namespaces/ns.yaml`

### Get all namespaces
`kubectl get namespaces`

### Deleting a namespace
`kubectl delete namespaces dev`


### To set default namespace
`kubectl config set-context --current --namespace=dev`

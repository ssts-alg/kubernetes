#### Create Configmap
`kubectl create configmap test-map --from-literal=vpc_id="vpc-12345" --from-literal=db_name=dev-db`

#### Create config map from file

`kubectl create -f config_map.yaml`
`kubectl create -f pod.yaml`

#### Describe configmap
`kubectl describe cm CONFIG_MAP_NAME`

### To validate
`kubectl exec -it myapp bash`
`cd /etc/dev-mount`
from here you can able to find the values

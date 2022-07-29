# kasten:
# ***Multicluster management***
## Requirement
## K3 cluster Installation :
```
$curl -sfL https://get.k3s.io | sh -
$export KUBECONFIG=/etc/rancher/k3s/k3s.yaml
$sudo chmod 644 $KUBECONFIG 
$kubectl get nodes
```

## K10 installation:
### Prerequisites :

```
$helm repo add kasten https://charts.kasten.io/
```
```
$kubectl create namespace kasten-io
```
```
$helm install k10 kasten/k10 --namespace=kasten-io
$kubectl annotate volumesnapshotclass \
 $(kubectl get volumesnapshotclass -o=jsonpath='{.items[?(@.metadata.annotations.snapshot\.storage\.kubernetes\.io\/is-default-class=="true")].metadata.name}') \
    k10.kasten.io/is-snapshot-class=true
```

## Validating the Install
```
$kubectl get pods --namespace kasten-io --watch
```

### Validate Dashboard Access
```
$kubectl --namespace kasten-io port-forward service/gateway 8080:8000
```
#### The K10 dashboard will be available at http://127.0.0.1:8080/k10/#/


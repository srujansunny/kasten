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

### Clusters
In a multi-cluster setup, one cluster is designated as primary, while all others are designated as secondaries.

##### TIP
The k10multicluster tool uses Kubernetes contexts available on the local system. To see the contexts available, use the following command:

```
$kubectl config get-contexts
```

#### Setup-Primary
To setup the primary cluster, use the setup-primary command:

```
$k10multicluster setup-primary \
    --context=<primary_cluster_context_name> \
    --name=<primary_cluster_name>
```

### K10 Multi-Cluster Manager dashboard

![image](https://user-images.githubusercontent.com/93370998/181757527-6ff3c9f4-f846-4d75-b4dd-f86f5665cee9.png)


### ADDING THE SECONDARY CLUSTER 
 
#### --add another cluster config file in add cluster-- 
![image](https://user-images.githubusercontent.com/93370998/181766141-8475479e-7efa-4786-8188-4201d9269158.png)


![image](https://user-images.githubusercontent.com/93370998/181765743-5116bde7-8ca4-4c19-b052-865e8eaf8bca.png)









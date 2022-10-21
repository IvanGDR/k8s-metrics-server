# K8S Metrics Server



Make sure nodes are up and running

```
$ kubectl get nodes
```
```
NAME               STATUS   ROLES           AGE   VERSION
ip-172-31-23-144   Ready    control-plane   60d   v1.24.0
ip-172-31-23-215   Ready    <none>          60d   v1.24.0
ip-172-31-25-163   Ready    <none>          60d   v1.24.0
ip-172-31-26-134   Ready    <none>          60d   v1.24.0
```


Install K8S Metrics Server

```
$ kubectl apply -f https://raw.githubusercontent.com/ACloudGuru-Resources/content-cka-resources/master/metrics-server-components.yaml
```
```

serviceaccount/metrics-server created
clusterrole.rbac.authorization.k8s.io/system:aggregated-metrics-reader created
clusterrole.rbac.authorization.k8s.io/system:metrics-server created
rolebinding.rbac.authorization.k8s.io/metrics-server-auth-reader created
clusterrolebinding.rbac.authorization.k8s.io/metrics-server:system:auth-delegator created
clusterrolebinding.rbac.authorization.k8s.io/system:metrics-server created
service/metrics-server created
deployment.apps/metrics-server created
apiservice.apiregistration.k8s.io/v1beta1.metrics.k8s.io created
```

Double Check It has been installed correctly

```
$ kubectl get --raw /apis/metrics.k8s.io/
```
```
{"kind":"APIGroup","apiVersion":"v1","name":"metrics.k8s.io","versions":[{"groupVersion":"metrics.k8s.io/v1beta1","version":"v1beta1"}],"preferredVersion":{"groupVersion":"metrics.k8s.io/v1beta1","version":"v1beta1"}}
```

Execute Metrics command on nodes

```
$ kubectl top nodes
```
```
NAME               CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%
ip-172-31-23-144   151m         7%     2248Mi          28%
ip-172-31-23-215   55m          2%     1172Mi          14%
ip-172-31-25-163   51m          2%     1124Mi          14%
ip-172-31-26-134   65m          3%     1485Mi          18%
```

Execute Metrics command on all namespaces

```
 $ kubectl top pods --all-na
mespaces
```
```
NAMESPACE     NAME                                       CPU(cores)   MEMORY(bytes)
default       nginx                                      0m           3Mi
kube-system   calico-kube-controllers-5b97f5d8cf-b9kvv   3m           43Mi
kube-system   calico-node-4vk5j                          21m          79Mi
kube-system   calico-node-92c7l                          24m          79Mi
kube-system   calico-node-lq6cw                          31m          96Mi
kube-system   calico-node-pg98p                          21m          94Mi
kube-system   coredns-6d4b75cb6d-hz2rn                   2m           13Mi
kube-system   coredns-6d4b75cb6d-s8bfx                   2m           13Mi
kube-system   etcd-ip-172-31-23-144                      12m          55Mi
kube-system   kube-apiserver-ip-172-31-23-144            43m          380Mi
kube-system   kube-controller-manager-ip-172-31-23-144   10m          49Mi
kube-system   kube-proxy-2r647                           1m           17Mi
kube-system   kube-proxy-2t648                           1m           13Mi
kube-system   kube-proxy-gbx42                           1m           17Mi
kube-system   kube-proxy-p55jt                           1m           13Mi
kube-system   kube-scheduler-ip-172-31-23-144            3m           18Mi
kube-system   metrics-server-78cd48fcdf-dq4w5            3m           16Mi
```

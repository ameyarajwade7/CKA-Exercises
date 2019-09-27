# 5% Networking

Use [KATAKODA](https://www.katacoda.com/courses/kubernetes/playground) for all the exercies


### Check wich netwok cni is deployed in the cluster

<details><summary>Answer</summary>
<p>

Generelly, network cni's are deployed as daemonset in kube-system namespace

```bash
kubectl get daemonset -n kube-system
```


```bash
NAMESPACE     NAME                  DESIRED   CURRENT   READY   UP-TO-DATE   AVAILABLE   NODE SELECTOR   AGE
kube-system   kube-keepalived-vip   1         1         1       1            1           <none>          18m
kube-system   kube-proxy            2         2         2       2            2           <none>          18m
kube-system   weave-net             2         2         2       2            2           <none>          18m
```
You can see here weave-net is network cni 
</p>
</details>

### Create a deployment name=pie image=nginx replicas=1 and expose it via a service

<details><summary>Answer</summary>
<p>


```bash
kubectl run pie --image=nginx --replicas=1 
kubectl expose deployment pie --port=80
```

</p>
</details>

### Create a pod image=busybox and access the pie service uging same pod 

<details><summary>Answer</summary>
<p>


```bash
kubectl run busybox --rm -ti --image=busybox /bin/sh

```
```bash
wget -O- pie
```

</p>
</details>

### Create a Network Policy so that pie service is only accesible to pod labeled with environment=prod 

<details><summary>Answer</summary>
<p>


```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: access-pie
spec:
  podSelector:
    matchLabels:
      run: pie
  ingress:
  - from:
    - podSelector:
        matchLabels:
          environment: "prod"
```
</p>
</details>

### Create two pods busybox one with label environment=prod and one without label and try to access pie service   

<details><summary>Answer</summary>
<p>

-Without label
```bash
kubectl run busybox --rm -ti --image=busybox /bin/sh

```
```bash
wget -O- pie
```
-With label
```bash
kubectl run busybox --labels=environment=prod --rm -ti --image=busybox /bin/sh

```
```bash
wget -O- pie
```
</p>
</details>
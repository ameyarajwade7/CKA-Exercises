# 5% Scheduling

Use [KATAKODA](https://www.katacoda.com/courses/kubernetes/playground) for all the exercies


### List all the node with its lables

<details><summary>Answer</summary>
<p>

```bash
kubectl get node --show-labels
```

</p>
</details>

### Label a node node01 with env=dev

<details><summary>Answer</summary>
<p>


```bash
kubectl label nodes node01 env=dev
```

</p>
</details>

### Create a pod nginx with image=nginx gets scheduled to node with label env=dev

<details><summary>Answer</summary>
<p>

```bash
# create a  YAML template with this command
kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml > pod.yaml
# update pod.yaml to add node selector as below
```

```YAML
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx
    imagePullPolicy: IfNotPresent
  nodeSelector:
    env: dev
```

</p>
</details>

### List all the taints key present on all nodes use jsonpath

<details><summary>Answer</summary>
<p>

```bash
kubectl get node -o jsonpath='{.items[*].spec.taints[*].key}'
```

</p>
</details>

### Taint a node node01 with key=env and value=prod, effect=NoSchedule

<details><summary>Answer</summary>
<p>

```bash
kubectl taint nodes node1 env=prod:NoSchedule
```

</p>
</details>

### Create a pod nagesh with image=nginx. It will not be scheduled on node01.

<details><summary>Answer</summary>
<p>

```bash
kubectl run nagesh --image=nginx --restart=Never 
```

</p>
</details>

### Update the pod nagesh with tolerence to the taint we have added earlier. It will be scheduled on node01.

<details><summary>Answer</summary>
<p>

```yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nagesh
  name: nagesh
spec:
  containers:
  - image: nginx
    name: nagesh
    resources: {}
  dnsPolicy: ClusterFirst
  tolerations:
  - key: "env"
    operator: "Equal"
    value: "prod"
    effect: "NoSchedule"
  restartPolicy: Never
status: {}

```

</p>
</details>
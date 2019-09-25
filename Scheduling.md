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
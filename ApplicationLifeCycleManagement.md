# 5% Application Lifecycle Management

Use [KATAKODA](https://www.katacoda.com/courses/kubernetes/playground) for all the exercies


### Create a deployment "mangesh" with image=nginx with 2 replicas 

<details><summary>Answer</summary>
<p>

```bash
kubectl run mangesh --image=nginx --replicas=3
```

</p>
</details>

### Scale up deployment mangesh to 6 replicas and Scale down to 1 replica, make sure your actions are "recorded"

<details><summary>Answer</summary>
<p>

```bash
kubectl scale deployment mangesh --replicas=6 --record
kubectl scale deployment mangesh --replicas=1 --record
```

</p>
</details>

### Check Scale up and scaledown action are recored

<details><summary>Answer</summary>
<p>

```bash
kubectl rollout history deployment mangesh
```

</p>
</details>

### Update image=nginx:alpine for deployment mangesh and make sure tour action is recored

<details><summary>Answer</summary>
<p>

```bash
kubectl set image deploy mangesh mangesh=nginx:alpine --record=true
```

</p>
</details>

### Label mangesh deployment as env=prod and make sure your action is recored

<details><summary>Answer</summary>
<p>

```bash
kubectl label deployment mangesh env=prod --record
```

</p>
</details>



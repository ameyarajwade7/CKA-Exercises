# 5% Application Lifecycle Management

Use [KATAKODA](https://www.katacoda.com/courses/kubernetes/playground) for all the exercies


### Create a deployment "apple" with image=nginx with 2 replicas 

<details><summary>Answer</summary>
<p>

```bash
kubectl run apple --image=nginx --replicas=3
```

</p>
</details>

### Scale up deployment apple to 6 replicas and Scale down to 1 replica, make sure your actions are "recorded"

<details><summary>Answer</summary>
<p>

```bash
kubectl scale deployment apple --replicas=6 --record
kubectl scale deployment apple --replicas=1 --record
```

</p>
</details>

### Check Scale up and scaledown action are recored

<details><summary>Answer</summary>
<p>

```bash
kubectl rollout history deployment apple
```

</p>
</details>

### Update image=nginx:alpine for deployment apple and make sure tour action is recored

<details><summary>Answer</summary>
<p>

```bash
kubectl set image deploy apple apple=nginx:alpine --record=true
```

</p>
</details>

### Label apple deployment as env=prod and make sure your action is recored

<details><summary>Answer</summary>
<p>

```bash
kubectl label deployment apple env=prod --record
```

</p>
</details>



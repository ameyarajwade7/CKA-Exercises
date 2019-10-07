# 19% Application Lifecycle Management

Use [KATAKODA](https://www.katacoda.com/courses/kubernetes/playground) for all the exercies


### Create a pod "apple" with image=nginx and label type=fruit

<details><summary>Answer</summary>
<p>

```bash
kubectl run --restart=Never apple --image=nginx -l type=fruit
```

</p>
</details>

### Create a service name "applesvc" which exposes pod apple (port 80)

<details><summary>Answer</summary>
<p>

```bash
kubectl expose pod  apple --name=applesvc --port=80
```

</p>
</details>

### Get apple pod's ip created in previous step, use a temp busybox image to wget its '/'

<details><summary>show</summary>
<p>

```bash
kubectl get po -o wide # get the IP, will be something like '10.1.1.131'
# create a temp busybox pod
kubectl run busybox --image=busybox --rm -it --restart=Never -- wget -O- 10.1.1.131:80
```

Alternatively you can also try a more advanced option:

```bash
# Get IP of the nginx pod
NGINX_IP=$(kubectl get pod nginx -o jsonpath='{.status.podIP}')
# create a temp busybox pod
kubectl run busybox --image=busybox --env="NGINX_IP=$NGINX_IP" --rm -it --restart=Never -- wget -O- $NGINX_IP:80
``` 

</p>
</details>

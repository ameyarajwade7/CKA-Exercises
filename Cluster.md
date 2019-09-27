# 8% Cluster

Use [KATAKODA](https://www.katacoda.com/courses/kubernetes/playground) for all the exercies


### Check current kubeadm version and plan for cluster upgrade  

<details><summary>Answer</summary>
<p>

you can see the current cluster and kubeadm version using following command

```bash
kubeadm upgrade plan
```

</p>
</details>

### Upgrade current kubeadm version to vesion 1.15.0-00  

<details><summary>Answer</summary>
<p>


```bash
apt-get upgrade -y kubeadm=1.15.0-00
```

</p>
</details>

### Upgrade and restart kubelet service  

<details><summary>Answer</summary>
<p>


```bash
apt-get upgrade -y kubelet=1.15.0-00
systemctl restart kubelet
```

Make sure master node is upgraded

```bash
kubectl get nodes

```
```bash
NAME      STATUS    ROLES     AGE       VERSION 
master    Ready     master    1d        v1.15.0
```

</p>
</details>

### Remove all the pods running on node node01 and mark it unschedulable
<details><summary>Answer</summary>
<p>


```bash
kubectl drain node noe01
```

</p>
</details>

### Backup etcd and store it in snapshotdb
- You need to install etcdctl first use latest from  https://github.com/etcd-io/etcd/releases
<details><summary>Answer</summary>
<p>

- Read more about at [ETCD Backup](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/#backing-up-an-etcd-cluster)

```bash
ETCDCTL_API=3 etcdctl snapshot save snapshotdb --endpoints=https://[127.0.0.1]:2379 --cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/healthcheck-client.crt --key=/etc/kubernetes/pki/etcd/healthcheck-client.key
```

</p>
</details>

### Verify etcd backup stored  in snapshotdb
- You need to install etcdctl first use latest from  https://github.com/etcd-io/etcd/releases
<details><summary>Answer</summary>
<p>

```bash
ETCDCTL_API=3 etcdctl --write-out=table snapshot status snapshotdb --endpoints=https://[127.0.0.1]:2379 --cacert=/etc/kubernetes/pki/etcd/ca.crt \
--cert=/etc/kubernetes/pki/etcd/healthcheck-client.crt --key=/etc/kubernetes/pki/etcd/healthcheck-client.key
```

</p>
</details>
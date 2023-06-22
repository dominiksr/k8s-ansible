# k8s-ansible
## Ubuntu 22.04 + k8s v1.27.2

1. Create "hosts" file.
```
[masters]
master ansible_host=172.31.117.172 ansible_user=ubuntu

[workers]
worker1 ansible_host=172.31.120.66 ansible_user=ubuntu
worker2 ansible_host=172.31.118.25 ansible_user=ubuntu
```

2. Test connection.
```
ansible -i hosts all -m ping
```

3. Copy keys and use sudo without needing a password.
```
ansible-playbook --ask-become-pass -i hosts users.yml
```

4. Install Kubernetes
```
ansible-playbook -i hosts install-k8s.yml
```

5. Create master node and Calico network.
```
ansible-playbook -i hosts master.yml
```

6. Join Worker Nodes to Kubernetes Cluster.
```
ansible-playbook -i hosts join-workers.yml
```


https://buildvirtual.net/deploy-a-kubernetes-cluster-using-ansible/

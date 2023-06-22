# k8s-ansible
## Ubuntu 22.04 + k8s(containerd) v1.27.2 + calico v3.26.1
### configuration:

ansible user with sudo privileges = ubuntu

cluster cidr = 10.10.0.0/16

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

3. Create user. Copy keys and use sudo without needing a password. 
```
ansible-playbook --ask-become-pass -i hosts users.yml #type master/worker password
```

4. Install Kubernetes and requirements.
```
ansible-playbook -i hosts install-k8s.yml
```

5. Create master node and Calico network. 
```
ansible-playbook --ask-become-pass -i hosts master.yml #type ansible host password
```

6. Join Worker Nodes to Kubernetes Cluster.
```
ansible-playbook -i hosts join-workers.yml
```

# TODO
- k alias
- kubectl autocompletion


links:

https://buildvirtual.net/deploy-a-kubernetes-cluster-using-ansible

https://docs.tigera.io/calico/latest/getting-started/kubernetes/self-managed-onprem/onpremises#install-calico

https://raw.githubusercontent.com/projectcalico/calico/v3.26.1/manifests/tigera-operator.yaml

https://raw.githubusercontent.com/projectcalico/calico/v3.26.1/manifests/custom-resources.yaml

# Build a Kubernetes cluster using k3s via Ansible.

Author: https://github.com/itwars

## K3s Ansible Playbook

Build a Kubernetes cluster using Ansible with k3s. The goal is easily install a Kubernetes cluster on machines running:

- [X] Debian 
- [ ] Ubuntu 
- [X] CentOS 

on processor architecture:

- [X] x64
- [X] arm64
- [X] armhf

## System requirements:

Deployment environment must have Ansible 2.4.0+
Master and nodes must have passwordless SSH access

## Usage

Add the system information gathered above into a file called hosts.ini. For example:

```
[master]
192.16.35.12

[node]
192.16.35.[10:11]

[k3s-cluster:children]
master
node
```

Start provisioning of the cluster using the following command:

```
ansible-playbook site.yml
```

## Kubeconfig

To get access to your **Kubernetes** cluster just scp debian@master_pi:~/kube/config ~/.kube/config

## K3s install helm

####download helm

```curl https://raw.githubusercontent.com/kubernetes/helm/master/scripts/get > install-helm.sh```

####Make instalation script executable

```chmod u+x install-helm.sh```

####Install helm

```./install-helm.sh```

#### cp /home/devops/.kube/config ~/.kube/config

#Create tiller service account
```kubectl -n kube-system create serviceaccount tiller```

####Create cluster role binding for tiller

```kubectl create clusterrolebinding tiller --clusterrole cluster-admin --serviceaccount=kube-system:tiller```

####Initialize tiller

```helm init --service-account tiller```



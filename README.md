# OpenShift KVM Lab

This repository is used to get an OpenShift lab running quickly on a fedora machine with enough horsepower to support a small 4 node cluster via Ansible. My laptop has ~20GB of RAM and that is sufficient to run this with the defaults.  
Since I am currently using Fedora 27, that is what this is written to run on, YMMV.

## Install Prerequisites

```bash
[user@host openshift-kvm-lab]$ sudo dnf -y install ansible @virtualization
```

## Deploying the Cluster

### Set RHSM credentials if using RHEL
```bash
[user@host openshift-kvm-lab]$ export RHSM_USERNAME=XXXXXXXXX
[user@host openshift-kvm-lab]$ export RHSM_PASSWORD=XXXXXXXXX
[user@host openshift-kvm-lab]$ export RHSM_POOL=XXXXXXXXX
```

### Run deployment playbook

```bash
[user@host openshift-kvm-lab]$ ansible-playbook -v deploy.yml | tee deploy.log
```

### Tearing it all down

```bash
[user@host openshift-kvm-lab]$ ansible-playbook -v -i hosts playbooks/teardown.yml | tee teardown.log
```

## Modifying OpenShift deployment

The ansible host file used to deploy OpenShift can be found at [roles/ansible_host/files/hosts](roles/ansible_host/files/hosts). It can be used to modify the OpenShift installation.

## SSH into machine

```bash
[user@host openshift-kvm-lab]$ cluster-ssh
```

## Run OpenShift Installer

```bash
[user@ans ~]$ ansible-playbook -v -i hosts openshift-ansible/playbooks/prerequisites.yml

[user@ans ~]$ ansible-playbook -v -i hosts openshift-ansible/playbooks/deploy_cluster.yml
```

## Start Cluster
A script ```~/bin/cluster-up``` that will start the cluster
```bash
[user@host ~]$ cluster-up
```

## Shutdown Cluster
A script ```~/bin/cluster-down``` that will shutdown the cluster
```bash
[user@host ~]$ cluster-down
```

## TODO:

* Allow deployment on CentOS of Origin
* Deploy separate disks for docker storage
* Generalize for arbitrary cluster versions
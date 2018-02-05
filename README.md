# OpenShift KVM Lab

This repository is used to get an OpenShift lab running quickly on a laptop with enough horsepower to support a small 4 node cluster via Ansible. My laptop has ~20GB of RAM and that is sufficient to run this with the defaults.  
Since I am currently using Fedora 27, that is what this is written to run on, YMMV.

## Install Prerequisites

```bash
[user@host openshift-kvm-lab]$ sudo dnf -y install ansible @virtualization
```

## Deploying the Cluster

### Run deployment playbook

```bash
[user@host openshift-kvm-lab]$ ansible-playbook -v -i hosts deploy.yml | tee deploy.log
```

### Tearing it all down

```bash
[user@host openshift-kvm-lab]$ ansible-playbook -v -i hosts playbooks/teardown.yml | tee teardown.log
```

## Modifying OpenShift deployment

The ansible host file used to deploy OpenShift can be found at [roles/ansible_host/files/hosts](roles/ansible_host/files/hosts). It can be used to modify the OpenShift installation.

## SSH into machine

```bash
[user@host openshift-kvm-lab]$ ssh -i .hosts/id_rsa 10.0.10.10
```
# OpenShift KVM Lab

This repository is used to get an OpenShift lab running quickly on a linux machine with enough horsepower to support a small 4 node cluster via Ansible. My laptop has 32GB of RAM and that is sufficient to run this with the defaults.

Your machine must have passwordless sudo rights.

## Install Prerequisites

```bash
sudo dnf -y install @virtualization python3-pip
sudo pip3 install ansible==2.6.11
sudo mkdir /usr/share/ansible
cd /usr/share/ansible
sudo git clone https://github.com/openshift/openshift-ansible.git
cd openshift-ansible
sudo git checkout release-3.11
```

## Deploying the Cluster

### Set RHSM credentials
```bash
export RHSM_USERNAME=
export RHSM_PASSWORD=
export RHSM_POOL=
```

### Run deployment playbook

```bash
[user@host openshift-kvm-lab]$ ./playbooks/deploy.yml | tee deploy.log
```

### Tearing it all down

```bash
[user@host openshift-kvm-lab]$ ./playbooks/teardown.yml -e '@vars/infrastructure.yml'
```

# Tags

Tags can be used to control what parts of the deployment get run

## Running specific OpenShift playbooks
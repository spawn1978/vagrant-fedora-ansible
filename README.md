# Install Openshift Cluster using ansible in a Fedora26 - VM provisioned by vagrant on Virtualbox

- Download Fedora Cloud image from [here](https://alt.fedoraproject.org/cloud/)
- Import the image as box into Vagrant 
```bash
vagrant box add fedora26 /path/to/your/Fedora-Cloud-Base-Vagrant-27-1.6.x86_64.box
```
- Start VM on Virtualbox
```bash
vagrant up
```

- Git clone `openshihift-ansible` 
```bash
git clone -b release-3.7 https://github.com/openshift/openshift-ansible.git
```

- Import RPMs of OpenShift
```bash
ansible-playbook -i inventory install-package.yaml -e openshift_node=masters
```

- Enable NetworkManager
```bash
ansible-playbook -i inventory playbook/enable_network-manager.yml -e openshift_node=masters
```

- Create OpenShift cluster
```bash
ansible-playbook -i inventory openshift-ansible/playbooks/byo/config.yml
```

- Enable NetworkManager
```bash
ansible-playbook -i inventory playbook/enable_cluster_admin.yml -e openshift_node=masters
```

- Setup persistence
```bash
ansible-playbook -i inventory playbook/setup_persistence.yml -e openshift_node=masters
```

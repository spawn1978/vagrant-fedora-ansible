# Fedora26 on Virtualbox

- Download Fedora Cloud image from [here](https://alt.fedoraproject.org/cloud/)
- Import the image as box into Vagrant 
```
vagrant box add fedora26 /path/to/your/Fedora-Cloud-Base-Vagrant-27-1.6.x86_64.box
```
- Start VM on Virtualbox
```
vagrant up
```

- Git clone `openshihift-ansible` 
```
git clone -b release-3.7 https://github.com/openshift/openshift-ansible.git
```

- Import RPMs of OpenShift
```bash
ansible-playbook -i inventory install-package.yaml -e openshift_node=masters
```

- Create OpenShift cluster
```
ansible-playbook -i inventory openshift-ansible/playbooks/byo/config.yml
```
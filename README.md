# Fedora26 on Virtualbox

 cvbngqs	1§§12nm8 - Import the image as box in Vagrant zn 
```
vagrant box add fedora26 /path/to/your/Fedora-Cloud-Base-Vagrant-27-1.6.x86_64.box
```
- Start VM on Virtualbox
```
vagrant up
```
- SSH to the vagrant machine to add your public key
```
vagrant ssh
sudo -i
vi ~/.ssh/authorized/keys and add your key
```

- Git clone `openshihift-ansible` 
```
git clone -b release-3.7 https://github.com/openshift/openshift-ansible.git
```

- Create OCP cluster
```
ansible-playbook -i inventory openshift-ansible/playbooks/byo/config.yml
```
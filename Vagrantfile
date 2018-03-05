$vmMemory = Integer(ENV['VM_MEMORY'] || 5000)

# Override the default VM name appearing within VirtualBox
$vmName = ENV['VM_NAME'] || "fedora26-openshift"

# Private IP address to be used between the Host and the Guest but also the Openshift Server
$vmPrivateIP = ENV['VM_PRIVATE_IP'] || "192.168.64.50"


Vagrant.configure("2") do |config|

  # Community Centos Box
  config.vm.box = "fedora26"

  # Top level domain
  $tld = "vagrant.ocp"

  config.landrush.enabled = true
  config.landrush.tld = $tld
  config.landrush.guest_redirect_dns = false
  config.landrush.host_ip_address = $vmPrivateIP

  config.vm.network "private_network", ip: $vmPrivateIP
  config.vm.hostname = $tld

  config.vm.provider "virtualbox" do |v|
    v.memory = $vmMemory
    v.cpus = 4
    v.name = $vmName
  end

  # Install Python 36
  config.vm.provision "shell", inline: "sudo yum install -y python36"

  # Upload Public key
  config.vm.provision "shell" do |s|
  ssh_pub_key = File.readlines("#{Dir.home}/.ssh/id_rsa.pub").first.strip
  s.inline = <<-SHELL
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
  SHELL
  end

  
  # Uncomment the following block if you have a playbook at devel/ansible/playbook.yml you want Vagrant to run on the guest for you
  # # Ansible needs the guest to have these
  # config.vm.provision "shell", inline: "sudo dnf install -y libselinux-python python2-dnf"
  #
  # config.vm.provision "ansible" do |ansible|
  #     ansible.playbook = "devel/ansible/playbook.yml"
  # end

end
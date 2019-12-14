Vagrant.configure("2") do |config|
 
  config.vbguest.auto_update = false
  
  config.vm.define"ansible" do |ansible|
    ansible.vm.box = "centos/7"
    ansible.vm.provider "virtualbox"
    ansible.vm.network "private_network", ip: "10.0.11.10"
    ansible.vm.network "forwarded_port", guest: 80, host: 8081
    ansible.vm.hostname = "ansible"
    ansible.vm.provider :virtualbox do |vb|
      vb.name = "ansible"
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
      end
    ansible.vm.provision :shell, inline: "yum install -y centos-release-scl && \
      yum update -y && \
      yum install -y rh-python36 && \
      scl enable rh-python36 bash && \
      yum install -y ansible vim wget && \
      yum install -y https://packages.chef.io/files/stable/chef-server/13.0.17/el/7/chef-server-core-13.0.17-1.el7.x86_64.rpm && \
      yum install -y https://yum.puppet.com/puppet6-release-el-7.noarch.rpm && \
      yum install -y puppetserver puppetdb"
    ansible.vm.provision :shell, inline: "setenforce 0", run: "always"
    ansible.vm.provision :shell, inline: "sudo -u vagrant ssh-keygen -b 2048 -t rsa -f /home/vagrant/.ssh/id_rsa -q -N ''"
    ansible.vm.provision "file", source: "ansible/files/hosts_file", destination: "~/"
    ansible.vm.provision "file", source: "ansible/files/sshd_config", destination: "~/"
    ansible.vm.provision "file", source: "ansible", destination: "~/"
    ansible.vm.provision :shell, inline: "sudo cp /home/vagrant/hosts_file /etc/hosts"
    ansible.vm.provision :shell, inline: "sudo cp /home/vagrant/sshd_config /etc/ssh/sshd_config"
    ansible.vm.provision :shell, inline: "systemctl restart sshd.service"
  end

## Hadoop Nodes
(1..2).each do |i|
  config.vm.define"master0#{i}" do |master|
    master.vm.box = "centos/7"
    master.vm.network "private_network", ip: "10.0.11.1#{i}"
    master.vm.hostname = "master0#{i}"
    master.vm.provider :virtualbox do |vb|
      vb.name = "master0#{i}"
      vb.customize ["modifyvm", :id, "--memory", "512"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
#    master.vm.provision :shell, inline: "yum update -y"
    master.vm.provision :shell, inline: "setenforce 0", run: "always"
    master.vm.provision "file", source: "ansible/files/hosts_file", destination: "~/"
    master.vm.provision "file", source: "ansible/files/sshd_config", destination: "~/"
    master.vm.provision :shell, inline: "sudo cp /home/vagrant/hosts_file /etc/hosts"
    master.vm.provision :shell, inline: "sudo cp /home/vagrant/sshd_config /etc/ssh/sshd_config"
    master.vm.provision :shell, inline: "systemctl restart sshd.service"
      end
    end
  end

  (1..3).each do |i|
    config.vm.define"data0#{i}" do |data|
      data.vm.box = "centos/7"
      data.vm.network "private_network", ip: "10.0.11.2#{i}"
      data.vm.hostname = "data0#{i}"
      data.vm.provider :virtualbox do |vb|
        vb.name = "data0#{i}"
        vb.customize ["modifyvm", :id, "--memory", "512"]
        vb.customize ["modifyvm", :id, "--cpus", "2"]
  #    data.vm.provision :shell, inline: "yum update -y"
      data.vm.provision :shell, inline: "setenforce 0", run: "always"
      data.vm.provision "file", source: "ansible/files/hosts_file", destination: "~/"
      data.vm.provision "file", source: "ansible/files/sshd_config", destination: "~/"
      data.vm.provision :shell, inline: "sudo cp /home/vagrant/hosts_file /etc/hosts"
      data.vm.provision :shell, inline: "sudo cp /home/vagrant/sshd_config /etc/ssh/sshd_config"
      data.vm.provision :shell, inline: "systemctl restart sshd.service"
        end
      end
    end

  config.vm.post_up_message = "Provision finished. :)"
end
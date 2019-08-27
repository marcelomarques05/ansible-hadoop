# Vagrant (MacOS) + Ansible + Wordpress

### This is a basic Vagrant file to setup 6 hosts:

- ansible
- namenode01
- namenode02
- datanode01
- datanode02
- datanode03

The Vagrant is installed in Mac OS and it's running with CentOS7

You need manually to copy the ssh keys from ansible host to all nodes.
(I know I can automate this, but for now, this is manual).

### Tech

* [Vagrant] - Up the VMs with VirtualBox!
* [Ansible] - Provisioning Everything! Oh Yeah!
* [Hadoop] - The Elephant!

### Installation

Ok, first thing, from your Vagrant host, let's up the nodes...

```sh
$ cd ansible-hadoop
$ vagrant up
# output expected:
# ... looooot of stuff.... then:
```

When this step finishes, you need to connect to ansible host and copy the ssh key to all nodes (password for vagrant user is vagrant)

```sh
$ vagrant ssh ansible
[vagrant@ansible ~]$ ssh-copy-id {one node per time...}
```

now let's start the game!! run the playbook:

```sh
[vagrant@ansible ~]$ 
```

### General Information

this is a basic install, config for vagrant, and hadoop for study purposes. Of course you can get this, improve and do whatever changes for your need. :)


[//]: # (These are reference links used in the body of this note and get stripped out when the markdown processor does its job. There is no need to format nicely because it shouldn't be seen. Thanks SO - http://stackoverflow.com/questions/4823468/store-comments-in-markdown-syntax)

   [Ansible]: <http://ansible.com>
   [Vagrant]: <http://vagrantup.com>
   [Hadoop]: <https://hadoop.apache.org>
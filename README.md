# Ansible-VPS-Environment
This repository contains the ansible playbooks to construct the necessary environment
of my machines in VPS(production) and local vagrant machines(staging).

The playbooks contain only some tasks to install OS-dependent libraries and docker swarm at the moment. The final goal is to encompass all the playbooks for my running applications in VPS such that I could quickly change VPS vendors if necessary.

## Some notes before using this...
1. All playbooks are targeting on centos7 currently; centos8 and other distribution may be supported in the future.
2. Recommended version of Ansible is 2.9 or above.
3. **virtualbox** will be the only provider used in 'Vagrantfile'.

## Usage of Vagrantfile
1. This file is used for vagrant to create machines; you can tailor it for your needs:
* ```N```: the number of machines to create, please modify the host name/memory/cpus in conditions and *provider* section accordingly.
* ```centos7.vm.box```: vagrant box name, you could find some [here](https://app.vagrantup.com/boxes/search).
* In section *provision*, a sample user and a ssh public key are added for later use in ansible.
Please remember to modify it according to your situation.
2. Execute ```vagrant up``` in the same directory as Vagrantfile. Please make sure you have vagrant installed before executing.

## Usage of playbooks
1. Make sure ansible is installed on your control machine.
2. Git clone or copy the repository to the control machine.
3. Modify the hosts information in files 'production' or 'staging'.
4. Execute ```ansible-playbook site.yml``` to start. Default inventory is 'staging', and you could change this behavior in file 'ansible.cfg'

## References
1. [Vagrant Documentation][]
2. [Ansible Documentation][]

[Vagrant Documentation]: https://www.vagrantup.com/docs/ "vagrant docs"
[Ansible Documentation]: https://docs.ansible.com/ansible/latest/index.html "ansible docs"


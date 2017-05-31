# DC/OS Ansible Modularized Installation


The purpose of the modularized playbook is to install DC/OS cluster components one at a time.

All inventory IPs are hardcoded in the hosts.ini file. 
The following files must be modified with the correct values:

- [hosts.ini](http://nas.ajway.kr:30000/erp-ta/dcos-install-playbooks/blob/master/module-playbook/hosts.ini)
- [group_vars/all](http://nas.ajway.kr:30000/erp-ta/dcos-install-playbooks/blob/master/module-playbook/group_vars/all)

* Notice the hosts.ini file has hostname set with ansible_host= override to public IP.

## Usage

The installation must be done in the following order:

1. **Common package installation**
```
$ ansible-playbook -i hosts.ini -u root  dcos-preinstall.yml
```

2. **Bootstrap node**
```
$ ansible-playbook -i hosts.ini -u root dcos-bootstrap.yml
```
3. **Master nodes**
```
$ ansible-playbook -i hosts.ini -u root dcos-master.yml
```
4. **Private agents**
```
$ ansible-playbook -i hosts.ini -u root  dcos-private-agent.yml
```

5. **Public agents**
```
$ ansible-playbook -i hosts.ini -u root dcos-public-agent.yml
```


## Customization

### Change DC/OS cluster

* Modify [hosts.ini](http://nas.ajway.kr:30000/erp-ta/dcos-install-playbooks/blob/master/module-playbook/hosts.ini) to change the cluster configuration.

* Modify the relevant `tasks` defined in the [roles](http://nas.ajway.kr:30000/erp-ta/dcos-install-playbooks/tree/master/module-playbook/roles) if there is a need to (optional).

### Install configuration parameters

* Modify the `install configuration` settings in [group_vars/all](http://nas.ajway.kr:30000/erp-ta/dcos-install-playbooks/blob/master/pc-playbook/group_vars/all) custom installation.

### Host variables

* Upon addition of a node, update host variables to [default](http://nas.ajway.kr:30000/erp-ta/dcos-install-playbooks/blob/master/module-playbook/roles/ansible-dcos-bootstrap-master/defaults/main.yml) in the relevant roles.

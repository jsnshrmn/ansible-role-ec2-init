OULibraries.ec2-init
=========

OULibraries EC2 init.

Requirements
------------

Uses the EC2 module, so the boto package is required. Now requires Ansible 2.x

Role Variables
--------------
You'll need to define at least one user in the 'users' var. eg.

```
users:
  - name: 'centos'
    groups: 'wheel,apache'
    keyname: 'aws-name-for-key'
    pubkey: 'ssh-rsa somepubkey centos@example.org'
```

The first user and key listed will be used to launch the instance. The first user's key key will be added to aws if it isn't already there.

Other vars that are the same across boxes:

ec2_vpc_id: The VPC to which you wish to apply the security groups
ec2_vpc_subnet_id: The VPC subnet to which you wish to deploy this machine
ec2_security_groups: the definition of the security groups you are using, eg.

```
ec2_security_groups:
  - name: out_all
    description: allow all outbound traffic
    rules: []
    rules_egress:
      - proto: all
        from_port: 0
        to_port: 65535
        cidr_ip: 0.0.0.0/0
  - name: in_ssh_broker
    description: allow inbound ssh from broker
    rules:
      - proto: tcp
        from_port: 22
        to_port: 22
        cidr_ip: 192.168.1.10/32
    rules_egress: []

```
See the docs for the ec2_group Ansible module for more info on managing groups.


ec2_instances: instance-unique info. tags and security groups. Will probably move more config into this later as currently, you can only spin up instances of the sames size.

ec2_tag_name should be the internal dns name of your instance. Note that this means that you either need to implement your own dns in aws, or you'll need to wrangle hosts files. 

ec2_security_group: a list of security group names to apply to this machine

```
ec2_instances:
  - ec2_tag_Name: app.workload.department.ec2.internal
    ec2_tag_App: DefaultApp
    ec2_tag_Unit: Default Unit
    ec2_tag_Workload: Development
    ec2_security_group: ['out_all', 'in_ssh_broker']
```

For the rest, see defaults/main.yml

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

License
-------

TBD

Author Information
------------------

Jason Sherman

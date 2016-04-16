OULibraries.ec2-init
=========

OULibraries EC2 init.

Requirements
------------

Uses the EC2 module, so the boto package is required.

Role Variables
--------------
You'll need to define one or more users in the 'users' var. eg.

```
users:
  - name: 'centos'
    groups: [centos, wheel]
    keyname: 'aws-name-for-key'
    pubkey: 'ssh-rsa somepubkey centos@example.org'
  - name: 'centos1'
    groups: 'wheel'
    pubkey: 'ssh-rsa anotherpubkey centos@example.org'
```

the specified key will be added to aws if it isn't already there.

ec2_vpc_subnet_id: The VPC subnet to which you wish to deploy this machine
ec2_key_name: The keypair name as listed in your aws console

For the rest, see defaults/main.yml

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

TBD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

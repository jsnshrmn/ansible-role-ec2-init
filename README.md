OULibraries.ec2-init
=========

OULibraries EC2 init.

Requirements
------------

Uses the EC2 module, so the boto package is required.

Role Variables
--------------
You'll need to define at least one user in the 'users' var. eg.

```
users:
  - name: 'centos'
    groups: [wheel]
    keyname: 'aws-name-for-key'
    pubkey: 'ssh-rsa somepubkey centos@example.org'
```

The first user and key listed will be used to launch the instance. The first user's key key will be added to aws if it isn't already there.

ec2_tag_name should be the internal dns name of your instance. Note that this means that you either need to implement your own dns in aws, or you'll need to wrangle hosts files. eg.

```
ec2_tag_Name: "app.workload.department.ec2.internal"
```

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

Jason Sherman

Ansible Role: wireguard-ssm
=========

Provide glue for reading and writing Wireguard configuration in AWS Systems Manager Parameter Store.

The idea behind this role is to have an off-host location to store a sinle Wireguard EC2 instance's public key. The requirements were:
* Replace OpenVPN
* Single Wireguard VPN endpoint per AWS region
* Make the endpoint instances ephemeral, store useful information off-host

There are intentions to extend this role to apply wireguard peer configuration which will be populated directly into Parameter Store.

Thanks to [githubixx](https://github.com/githubixx) and contributors for [ansible-role-wireguard](https://github.com/githubixx/ansible-role-wireguard).

Requirements
------------

A running EC2 instance with an IAM policy assigned which will allow read/write access to AWS SSM Parameter Store.

This module requires the following:

    collections:
      - name: amazon.aws
        version: 1.4.0
      - name: community.aws
        version: 1.3.0




Role Variables
--------------

Customisable variables have been declared in `defaults/main.yml`.

The base directory for Parameter Store:

      wireguard_ssm_base_path: "/wireguard"

Deploying this on an `us-east-1` instance, will create the following parameter path:

      /wireguard/us-east-1/public_key

Dependencies
------------

You will need a running instance of Wireguard on the EC2 instance and a policy assigned to the EC2 instance's role which will permit read/write access to SSM Parameter Store, ideally you have limited it to the value of `wireguard_ssm_base_path`.

Although this role does not explcitly depend on [githubixx.ansible-role-wireguard](https://github.com/githubixx/ansible-role-wireguard), it was used in the testing.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    hosts:
      localhost:
      roles:
        - role: gavmain.wireguard-ssm
          vars:
            wireguard_ssm_base_path: /wireguard

License
-------

MIT

Author Information
------------------

This role was created in 2021 by [Gav Main](https://github.com/gavmain).

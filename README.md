module reference

https://paloaltonetworks.github.io/pan-os-ansible/modules/panos_security_rule_module.html


前提
・PA-3220にACLを追加するジョブテンプレート「aclTest job」が想定通りに動作しない（エラーが出る）


//念のための paloaltonetworks.panos
[admin@ansible ~]$
[admin@ansible ~]$ sudo ansible-galaxy collection install paloaltonetworks.panos
[sudo] admin のパスワード:
Starting galaxy collection install process
Process install dependency map
Starting collection install process
Downloading https://galaxy.ansible.com/download/paloaltonetworks-panos-3.0.0.tar.gz to /root/.ansible/tmp/ansible-local-864557yhzruv1a/tmpemih029_/paloaltonetworks-panos-3.0.0-40fae3dx
Installing 'paloaltonetworks.panos:3.0.0' to '/root/.ansible/collections/ansible_collections/paloaltonetworks/panos'
paloaltonetworks.panos:3.0.0 was installed successfully
[admin@ansible ~]$


[admin@ansible ~]$
[admin@ansible ~]$ sudo ansible-galaxy collection install -r /var/lib/awx/projects/collection/requirements.yml -p ./
Starting galaxy collection install process
[WARNING]: The specified collections path '/home/admin' is not part of the configured Ansible collections paths '/root/.ansible/collections:/usr/share/ansible/collections'. The installed collection won't be picked up in an Ansible run.
Process install dependency map
ERROR! Failed to resolve the requested dependencies map. Could not satisfy the following requirements:
* cisco.nxon:* (direct request)
[admin@ansible ~]$


ERROR! couldn't resolve module/action 'paloaltonetworks.panos.panos_security_rule'. This often indicates a misspelling, missing collection, or incorrect module path.
The error appears to be in '/runner/project/palo_acl.yml': line 5, column 7, but may
be elsewhere in the file depending on the exact syntax problem.


---
- connection: local
  gather_facts: false
  tasks:
    - name: testacl-ping
      paloaltonetworks.panos.panos_security_rule:
        provider: '{{ provider }}'
        ip_address: "10.44.229.102"
        password: "Palopassword01"
        username: "admin"
        operation: 'create'
        rule_name: 'testACL'
        source_zone: ['vlan2']
        destination_zone: ['vlan3']
        vsys: 'vsys1'
        source_ip: ['192.168.2.1']
        destination_ip: ['192.168.3.1']
        application: ['any']
        commit: 'yes'

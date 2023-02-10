orion-node-manage
=========

This role provides the orion_node_manage module for unmanaging, remanaging, and decommissioning nodes in Orion. It can be used to suppress alerts during maintenance of Orion managed systems.
For more info please see the module file located in ./library/orion_node_manage.py.

Requirements
------------

This module will install all pip packages to the controller node needed by the module.


Example Playbook
----------------

I recommend running this on the local node as follows:

    - name: Setup Local Solarwinds
      hosts: localhost
      gather_facts: no
      roles:
          - { role: asagage.orion-node-manage }

    - name: Solarwinds Manage Nodes
      hosts: all
      tasks:
        - name: Unmanage node via IP Address
          orion_node_manage:
            ip_address: hostvars[inventory_hostname]['ansible_default_ipv4']['address']
            state: unmanaged
            username: "{{ sw_username }}"
            password: "{{ sw_password }}"
            hostname: "{{ sw_hostname }}"
          delegate_to: FQDN of tower/AAP system

        - name: Unmanage node via DNS Name
          orion_node_manage:
            dns_name: "{{inventory_hostname}}"
            state: unmanaged
            username: "{{ sw_username }}"
            password: "{{ sw_password }}"
            hostname: "{{ sw_hostname }}"
          delegate_to: FQDN of tower/AAP system

        - name: Remanage node via IP Address
          orion_node_manage:
            ip_address: hostvars[inventory_hostname]['ansible_default_ipv4']['address']
            state: managed
            username: "{{ sw_username }}"
            password: "{{ sw_password }}"
            hostname: "{{ sw_hostname }}"
          delegate_to: FQDN of tower/AAP system

        - name: Remanage node via DNS Name
          orion_node_manage:
            dns_name: "{{inventory_hostname}}"
            state: managed
            username: "{{ sw_username }}"
            password: "{{ sw_password }}"
            hostname: "{{ sw_hostname }}"
          delegate_to: FQDN of tower/AAP system

        - name: Decommission node via IP Address
          orion_node_manage:
            ip_address: hostvars[inventory_hostname]['ansible_default_ipv4']['address']
            state: decommissioned
            username: "{{ sw_username }}"
            password: "{{ sw_password }}"
            hostname: "{{ sw_hostname }}"
          delegate_to: FQDN of tower/AAP system

License
-------

MIT

Author Information
------------------

Asa Gage @asagage

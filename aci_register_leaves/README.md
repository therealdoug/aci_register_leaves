aci_register_leaves
=========

Provided Node IDs, this role will query the APIC for the Node names and OOB MGMT IPs and then register them in DNS.

Requirements
------------

- Leaves need to be registered in the fabric.  
  - Future versions will do this for you with provided serial numbers.
- This role shares the user/pass that logs into the APIC. So, that same user/pass should have RW access to Infoblox.

Role Variables
--------------

  **node1**: The first node in a Leaf pair. Will always be an odd number.
  **node2**: The second node in a Leaf pair.  Will always be an even number.
  **pod**: The pod that these leaves live in.  Should be the same as the first number of Node ID
  **site**: This is the site code that corresponds to the pod.  This is used to make sure the A record has the correct FQDN.

Dependencies
------------

This role will typically be run before or after the **add_vpc_leaf_pair** role.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```
- hosts: localhost
  gather_facts: false
  
  vars:
    nodes:
      - { node1: "111", node2: "112", pod: "1" , site: "XXX" }
      - { node1: "113", node2: "114", pod: "2" , site: "YYY" }
      
  tasks:
    - include_role:
        name: aci_register_leaves
      with_items: '{{ nodes }}'
```
License
-------

BSD

Author Information
------------------


# Ansible
Automates the management of remote systems and controls their desired state

## Intro
1. uses playbooks (ie. scripts) to automate tasks, and ensures systems remain in desired state
1. agent-less, scalable, flexible
1. decentralized, uses ssh with existing credentials
1. does not change anything if state is in good standing

## Environment
Consists of three things:
1. Control Node
    - node where ansible is installed
1. Inventory
    - list of managed nodes that are logically organized
1. Managed Nodes
    - remote system that ansible controls

## Building an Inventory
Prerequisites: needs ip or FQDN (fully qualified domain name), as well as ssh access to host(s) \
- example .ini inventory
    ```ini
        [myhosts]
        x.x.x.x
        x.x.x.x
    ```
- example .yaml file
    ```yaml
    groupname:
        children:
            host1:
                ansible_host: x.x.x.x
                var0: val
            host2:
                ansible_host: x.x.x.x
                var0: val
        groupvar:
            var1: val
            var2: val
    ```
  - variables can apply to specific hosts or all hosts in group\
To verify inventory file `ansible-inventory -i inventory.ini --list` \
To ping myhoosts group in inventory: `ansible myhosts -m ping -i inventory.ini` \
`-u`option if username is different on control node vs managed ndoes


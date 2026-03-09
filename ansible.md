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
Prerequisites: needs ip or FQDN (fully qualified domain name), as well as ssh access to host(s)
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
- variables can apply to specific hosts or all hosts in group

To verify inventory file `ansible-inventory -i inventory.ini --list`

To ping myhoosts group in inventory: `ansible myhosts -m ping -i inventory.ini`

`-u` option if username is different on control node vs managed ndoes

## Creating a Playbook
Playbook
- list of plays that define the order in which Ansible performs actions

Play
- Ordered list of tasks that maps to nodes in an invenotry

Task
- reference to single node module that defiens operations that sible performs

Module
- unit of code or binary that Ansible runs on managed nodes

Example:
```yaml
- name: playname
  hosts: hosts
  tasks:
    - name: ping
      ansible.builtin.ping:

    - name: print message
      ansible.builtin.debug:
        msg: Hello
```
To run: `ansible-playbook -i inventory.yml playbook.yml`

## Playbook Commands
Disable gather_facts:
- `gather_facts: false`
- gather facts will automatically run in a play and gathers system info, hardware details, network info, nevironment variables, and ansible specific variables, will error out if system does not have python3 package fully installed

Run raw commands: 
- `raw: <command>`
- will create a changed state when running raw commands, use: `changed_when: false` to show `ok` instead of `changed`

Run command if condition is met:
- `when <condition>`

Save variables:
- `register: <var>`
- can be used in conjunction with `when`

Disable changed state:
- `changed_when: false` 

Run play when certain condition is met
- '`when: <var/condition>`

Ignore unreachable error:
- `ignore_uncreachable: yes`
- If running commands like `reboot now` that immediately close ssh connection

Retry:
- `retry: <times>`
- can be used in cunjunction with `delay` and `until`

Delay:
- `delay: <seconds>`

Until:
- `until: "'<text>' in <var>"`
- example if using register for result of raw command: `until: "'Success' in var.stdout"`

Wait for ssh connection on the host

    tasks:
      - name: wait for host ssh connection
        ansible.builtin.wait_for:
          host: "{{ inventory_hostname }}"
          port: 22
        delegate_to: localhost


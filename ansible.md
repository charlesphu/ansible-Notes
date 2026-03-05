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



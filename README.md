# Overview

Ansible playbooks to install and configure Neo4j graph database.

## Installation

Execute the shell script in the `extension` directory to install
and configure Ansible before running below commands

```sh
chmod +x extension/setup/setup.sh
./extension/setup/setup.sh
```

## CLI

### Encrypt/decrypt ansible vault file

A vault file contains sensitive information so that we shouldn't commit to source control in plaintext.
So we need to encrypt it before committing to source control. Using [Ansible vault](https://docs.ansible.com/ansible/latest/user_guide/vault.html#decrypting-encrypted-files) so this problem.

Run below command to decrypt vault.yml file in the inventory directory

```sh
ansible-vault decrypt inventories/dev/group_vars/vault.yml --vault-password-file ansible-vault.pass
```

Make change required for your setting and encrypt using below command

```sh
ansible-vault encrypt inventories/dev/group_vars/vault.yml --vault-password-file ansible-vault.pass
```

### Install and configure Neo4j Server

* Install Neo4j single server by running below command

Run below command to deploy a single Neo4j instance for `dev` environment.
Replace `dev` to any existing inventory in the `inventories` directory (i.e. staging, prod)

```sh
ansible-playbook neo4j.single.yml -e env=dev --vault-password-file ansible-vault.pass

#  or we can use -b -K to enter SUDO password (sudo su)
ansible-playbook neo4j.single.yml -e env=dev --vault-password-file ansible-vault.pass -b -K
```

## NOTE - you shouldn't check in the ansible-vault.pass file to source control

# Infra Playbooks

This repository will hold playbooks for my pc and servers using ansible.

## 1. Requirements

### 1.1 General requirements

This setup assumes that you have key based ssh access to your server.
To setup a new key, you can use the following.

* Generate a new ssh key

    ```sh
    ssh-keygen -t ed25516 -a 128 -f ~/.ssh/enter_your_custom_name
    ```

*Note: You can use the ```-t rsa -b 4096``` option instead of ```-t ed25519``` to generate a key with comparable security and better compatibility at the price of creation and login performance*

* Copy the ssh key to your server

    ```sh
    ssh-copy-id -i /path/to/your/private/key/file username@ip_address
    ```

## 1.2 Set user as password less sudo

Edit your sudoers file with and edit the line 50 to add passwordless sudo access to sudo group:

```sh
sudo visudo
change this -> %sudo   ALL=(ALL:ALL) NOPASSWD: ALL
```

### 1.3 Install Ansible


Install required python packages:

```sh
sudo apt install python3-venv
```

Create a virtual environment:

```sh
python -m venv .venv
```

Install required python modules:

```sh
python -m pip install -U -r requirements.txt
```

Activate your venv

```sh
source .venv/bin/activate (or activate.fish or activate.csh)
```

If you use VSCode, add your configuration to your VSCode folder or worksace settings

```json
"settings": {
		"ansible.python.activationScript": "./.venv/bin/activate"
}
```

### 1.4 Install ansible-galaxy requirements

Install the ansible requirements:

```sh
ansible-galaxy install -r requirements.yml
```

### 1.5 Creating a secret vault

Create a new secret vault with ansible:

```sh
ansible-vault create /secret/folder/path/vault.yml
```

### 1.6 Extra variables

Check for variable staring with "vault_" in the vars files.

## 2. Using the ansible playbook

Run the playbook:

```sh
ansible-playbook home.yml -i production.yml
```

## Credits/Sources

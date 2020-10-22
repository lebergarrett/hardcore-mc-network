# mc-network

Minecraft Server network using Ansible, Docker Containers, and possibly more in the future.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. To simplify my instructions, I will be writing it as if you are using a debian-based system. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

Ansible needs to be installed on the 'client' workstation, though in the current configuration both client and server are localhost.

```
sudo apt install ansible
```

### Installing

To get your environment running, you can go ahead and clone this repo locally using:

```
git clone https://github.com/imkumpy/mc-network.git
```

Once cloned, you will need to remove the existing vars/vault.yaml file and create your own that contains the info for MariaDB which will be used by LuckPerms (a spigot permissions plugin) so all your servers have a central location to make permissions changes.

```
rm vars/vault.yaml
ansible-vault create vars/vault.yaml
```

it will prompt you for a password, go ahead and set it to whatever you like. You will need to enter this whenever you run the playbook in the future, so make sure its something you remember.

Docker and docker-compose will need to be installed. There is a role in the playbook that should accomplish this on most os_families (currently commented out), but if you are like me and use Pop! OS you will need to accomplish this prior using the docker documentation (or modify the ansible role as needed).

The included 'requirements.yml' file can be used to install the roles and collections that are used by ansible for this playbook. Run the following command to install them:

```
ansible-galaxy install -r requirements.yml
```
For some reason the collection "community.general" which is included in the requirements file does not install, so that will need to be done manually

```
ansible-galaxy collection install community.general
```

Once that is done, you can modify the docker-compose config by editing host_vars/localhost.yml. The ansible formatting is very similar to docker-compose by default, and there is plenty in there by default so it should hopefully be easy to understand. The following is what will need to be changed at a minimum:

```
mc_ops: 'Jeb_,Dinnerbone'
mc_whitelisted_players: 'Jeb_,Dinnerbone'
```

## Deployment

To run the playbook, simply type the following while in the working dir:

```
ansible-playbook --ask-vault-pass playbook.yml
```

It will prompt for you vault password. That's it, your server network should be running! This can be verified with:

```
docker container ls
```

# mc-network

Minecraft Server network using Ansible, Docker COntainers, and possibly more in the future

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

Ansible needs to be installed on the 'client' workstation, though in all of the current configuration both client and server are localhost.

```
sudo apt install ansible
```

Docker and docker-compose will also need to be installed. There is a role in the playbook that should accomplish this on most os_families, but if you are like me and use Pop! OS you will need to accomplish this prior using the docker documentation (or modify the ansible role as needed)

The included 'requirements.yml' file can be used to install the roles and collections that are used by ansible for this playbook. Run the following command to install them:

```
ansible-galaxy install -r requirements.yml
```

### Installing

To get your environment running, you can go ahead and clone this repo locally using

```
git clone https://github.com/imkumpy/mc-network.git
```

Once cloned, you will need to create your own vars/vault.yaml that contains the info for a MariaDB which will be used by LuckPerms (a spigot permissions plugin) so all your servers have a central location to make permissions changes

```
ansible-vault create vars/vault.yaml
```

it will prompt you for a password, go ahead and set it to whatever you like. You will need to enter this whenever you run the playbook in the future, so make sure its something you remember.

Once that is set, you can modify the docker-compose config by editing host_vars/localhost.yml. The ansible formatting is very similar to docker-compose by default, and there is plenty in there by default so it should hopefully be easy to understand. The following is what will need to be changed at a minimum:

```
docker_users: 'your local user here'
mc_ops: 'your mc user here'
mc_whitelisted_players: 'your mc user here'
```

## Deployment

To run the playbook, simply type the following while in the working dir:

```
ansible-playbook --ask-vault-pass playbook.yml
```

This will output a docker-compose.yml file in your working dir, which you can run by typing:

```
docker-compose up -d
```

That's it, your server network should be running!

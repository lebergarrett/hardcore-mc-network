# mc-network
Minecraft Server network using Ansible, Docker Containers, and possibly more in the future

The playbook requires a file named vault.yaml to be created that contains the variables for MariaDB.
Use "ansible-vault create vars/vault.yaml" to do this. It will prompt for a password and then throw you in your $EDITOR (default is vi)

The vars that need to be set are:
 mysql_root  # The root pw for the db
 mysql_db  # The name of the db
 mysql_user  # The user for the db
 mysql_pass  # The user's pw for the db


Build the network out using the command:
 ansible-playbook --ask-vault-pass playbook.yml
it will ask for your vault password, supply the one you set when creating the vault above.

When the playbook is done, a docker-compose file will be dropped in the current working directory

To start the server network, simply run:
 docker-compose up -d

# Install Ansible
mac: brew install ansible
ubuntu: sudo apt install ansible

# Run Script 

cp  group_vars/secrets.yml group_vars/all.yml 
export ANSIBLE_VAULT_PASSWORD_FILE=/tmp/.vault_pass
echo verySecretPassword > /tmp/.vault_pass
ansible-vault encrypt group_vars/all.yml

ansible-playbook -i inventory.yml playbook_base.yml 

ansible-playbook -i inventory.yml playbook_manager.yml -e "username=site1user mariadb_user_password=lol"

# Roles

## secure_components

- Install Secure components (Fail2Ban, UFW)
- Configure Secure components (Fail2Ban, UFW) 

## web_components
- Install Web components (Nginx, MariaDB)
- Configure Nginx, MariaDB


## manager_create

- Create User
- Create FPM 
- Create www dir 
- Configure new site on Nginx
- Create an MariaDB user & database
- Configure certbot (Autosign certificates can be done for debug)
- TODO: Unzip & move php files if env PRE_CONSTRUCT_DIR is set, can be different for each site (WP, HelloWorld PHP files, etc.)
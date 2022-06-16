# webmethods-ansible-api-gateway --  Preparation steps

Preparation steps!!

## Authors

Fabien Sanglier
- Emails: [@Software AG](mailto:fabien.sanglier@softwareag.com) // [@Software AG Government Solutions](mailto:fabien.sanglier@softwareaggov.com)
- Github: 
  - [Fabien Sanglier](https://github.com/lanimall)
  - [Fabien Sanglier @ SoftwareAG Government Solutions](https://github.com/fabien-sanglier-saggs)

## Get the project's code

Get the project on the ansible server:

```bash
git clone https://github.com/softwareag-government-solutions/webmethods-ansible-api-gateway.git
```

## Fetch the supporting Ansible roles

The playbooks in this projects rely on many common Ansible roles for SoftwareAG.

Get the roles on the ansible server (and save them in folder "$HOME/ansible-sag-roles"):

```bash
mkdir -p $HOME/ansible-sag-roles \
    && cd $HOME/ansible-sag-roles \
    && git clone https://github.com/SoftwareAG/sagdevops-ansible-common.git \
    && git clone https://github.com/SoftwareAG/sagdevops-ansible-common-webmethods.git \
    && git clone https://github.com/SoftwareAG/sagdevops-ansible-apigateway.git \
    && git clone https://github.com/SoftwareAG/sagdevops-ansible-developer-portal.git \
    && git clone https://github.com/SoftwareAG/sagdevops-ansible-apiportal.git \
    && git clone https://github.com/SoftwareAG/sagdevops-ansible-apidatastore.git
```

or update them if already on the server:

```bash
cd $HOME/ansible-sag-roles/sagdevops-ansible-common && git pull \
    && cd $HOME/ansible-sag-roles/sagdevops-ansible-common-webmethods && git pull \
    && cd $HOME/ansible-sag-roles/sagdevops-ansible-apigateway && git pull \
    && cd $HOME/ansible-sag-roles/sagdevops-ansible-developer-portal && git pull \
    && cd $HOME/ansible-sag-roles/sagdevops-ansible-apiportal && git pull \
    && cd $HOME/ansible-sag-roles/sagdevops-ansible-apidatastore && git pull \
    && cd $HOME/customer_ssa_devops/ansible && git pull
```

## Ansible Vault password

To accomodate the commands with vault, let's create a password file for simplicity sake:

```bash
echo -n "vault password: "; read -s password; echo "$password" > $HOME/ansible_pass
```
+

```bash
chmod 600 $HOME/ansible_pass
```

NOTE: The default ansible vault password for this project is "supersecret"

## Setup SSH keys for Servers SSH access by Ansible

Make sure to add the SSH key that will be used by ansible to SSH connect to the target servers:

```bash
cat <<EOF > ~/.ssh/id_rsa
<PRIVATE SSH KEY>
EOF
chmod 600 ~/.ssh/id_rsa
```

Ensure SSH connectivity is available using that SSH key.

## Check connectivity

```bash
ansible all -m ping
```

## Install python3

```bash
ansible all --become -m raw -a "yum install -y python3"
```


______________________
These tools are provided as-is and without warranty or support. They do not constitute part of the Software AG product suite. Users are free to use, fork and modify them, subject to the license agreement. While Software AG welcomes contributions, we cannot guarantee to include every contribution in the master project.
_____________
For more information you can Ask a Question in the [TECHcommunity Forums](http://tech.forums.softwareag.com/techjforum/forums/list.page?product=webmethods).

You can find additional information in the [Software AG TECHcommunity](http://techcommunity.softwareag.com/home/-/product/name/webmethods).
_____________
Contact us at [TECHcommunity](mailto:technologycommunity@softwareag.com?subject=Github/SoftwareAG) if you have any questions.

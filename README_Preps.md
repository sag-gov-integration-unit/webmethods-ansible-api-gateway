# webmethods-ansible-api-gateway --  Preparation steps

Preparation steps!!

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

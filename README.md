# webmethods-ansible-api-gateway
A starter project to automate with Ansible the tasks related to APIGateway platform

This project makes use of various common Ansible roles available at [github.com/SoftwareAG](https://github.com/SoftwareAG) (search for "ansible")
For more details, go to [Preparation Steps](./README_Preps.md)

## Authors

Fabien Sanglier
- Emails: [@Software AG](mailto:fabien.sanglier@softwareag.com) // [@Software AG Government Solutions](mailto:fabien.sanglier@softwareaggov.com)
- Github: 
  - [Fabien Sanglier](https://github.com/lanimall)
  - [Fabien Sanglier @ SoftwareAG Government Solutions](https://github.com/fabien-sanglier-saggs)

## Preparation steps

Refer to [Preparation Steps](./README_Preps.md) to setup the solution on your Ansible Server.

## Running the playbooks

This section will run the commands one-by-one... but all could surely be assembled in a single automated "play" as needed!

### 0) Load target env

You may create an alias to run these commands quicker...
ie. for the UAT env:

```bash
alias run_ansible_uat="ansible-playbook -i ./environments/nonprod/uat/inventory --vault-password-file $HOME/ansible_pass
```


### 1) Sysprep all machines

The sysprep playbook will update the OS settings to make sure proper operation for the SoftwareAG products:

- System settings (ulimits, sysctl)
- OS firewall rules
- Install some packages (yum)
- Create SAG user
- Create SAG directory + assign permissions/ownership

```bash
run_ansible_uat do_sysprep.yaml
```

##### 2) Install all products

This playbook will perform the following:

- pull down the artifacts from the local product repository (ie. AWS S3, or internal file repo server):
    - SAG installer, SAG Image file, SAG Installation Script) 
- run silent installer with the right artifacts pulled from the file repo

```bash
run_ansible_uat do_install_products.yaml
```

##### 3) Update/Patch all products

This playbook will perform the following:

- pull down the Update artifacts from the local product repository (ie. AWS S3, or internal file repo server):
    - SAG Update Manager (SUM), SAG Patch Image file, SAG Patch SUM Script) 
- run SUM install
- run silent SUM patching operation with the right artifacts pulled from the file repo

```bash
run_ansible_uat do_patch_products.yaml
```

##### Configure API Datastore Clustering

This playbook will perform the needed file system operations to create a functionning API Datastore cluster.

```bash
run_ansible_uat workflow_apidatastore_clustering.yaml
```

##### Configure Terracotta Clustering (optional, only if APIGateway clustering with Terracotta)

This playbook will perform the needed file system operations to create a functionning Terracotta cluster.
NOTE: This is optional in versions >10.11, only needed if clustering with Terracotta is desired.

```bash
run_ansible_uat workflow_terracotta_clustering.yaml
```

##### Configure API Gateway Clustering - Option 1: Ignite Peers

This playbook will perform the needed file system operations to create a functionning API Gateway cluster 
ie. connected to API Datastore cluster + to its other API Gateway Ignite Peers


```bash
run_ansible_uat workflow_apigateway_clustering.yaml
```

##### Configure API Gateway Clustering - Option 2: Terracotta

If you want to do the clustering with Terracotta instead of ignite, run this playbook instead:

```bash
run_ansible_uat workflow_apigateway_clustering_with_terracotta.yaml
```

##### Configure API Gateway Various Settings 

This playbook will perform the following configuration items:

- update admin password
- set ssl certs (keystore, truststore)
- set ports (different types - http, https, internal, external)
- set extended settings
- set ldap
- set loadbalancer urls
- set promotion stages
- create users
- create groups and assign the users
- create teams and assign the groups
- import apigateway archive
- set api plans
- set api packages
- set aliases
- set api applications
- set apiportal destination
- publish apis to apiportal
- publish api packages to apiportal


```bash
run_ansible_uat configure_apigateway_settings.yaml
```


______________________
These tools are provided as-is and without warranty or support. They do not constitute part of the Software AG product suite. Users are free to use, fork and modify them, subject to the license agreement. While Software AG welcomes contributions, we cannot guarantee to include every contribution in the master project.
_____________
For more information you can Ask a Question in the [TECHcommunity Forums](http://tech.forums.softwareag.com/techjforum/forums/list.page?product=webmethods).

You can find additional information in the [Software AG TECHcommunity](http://techcommunity.softwareag.com/home/-/product/name/webmethods).
_____________
Contact us at [TECHcommunity](mailto:technologycommunity@softwareag.com?subject=Github/SoftwareAG) if you have any questions.

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

```bash
run_ansible_uat do_sysprep.yaml
```

##### 2) Install all products

```bash
run_ansible_uat do_install_products.yaml
```

##### 3) Update/Patch all products

```bash
run_ansible_uat do_patch_products.yaml
```

##### Configure Terracotta Clustering

```bash
run_ansible_uat workflow_terracotta_clustering.yaml
```

##### Configure API Datastore Clustering

```bash
run_ansible_uat workflow_apidatastore_clustering.yaml
```

##### Configure API Gateway Clustering

```bash
run_ansible_uat workflow_apigateway_clustering.yaml
```

##### Configure Gateway Settings 

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

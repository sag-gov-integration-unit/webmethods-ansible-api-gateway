# webmethods-ansible-api-gateway
A starter project to automate with Ansible the tasks related to APIGateway platform

supersecret

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

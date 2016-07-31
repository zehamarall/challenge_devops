# Challenge_devops

Este projeto visa criar, provisionar e deploy um servidor Web utilizando vagrant e ansible. Este projeto foi dividido em dois diretórios **ops** e **dev**.
O diretórios **ops** contém as informações de criação do ambiente. Já os diretório **dev** contém o src do projeto em nodejs e também o deploy e o roolback do Webapp.

## Requirements

 - Vagrant
 - Ansible 
 
## Quick Start

### Step One 

Entrar no diretório **ops** e criar o anbiente:

``` cd ops ```

``` vagrant up ```


### Step Two

Fazer um deploy da aplição utilizando Ansible:

```ansible-playbook --inventory-file=$PWD/ops/.vagrant/provisioners/ansible/inventory -vv dev/deploy/main.yml```


### Step Three

Fazer um Rollback do deploy anterior da aplição utilizando Ansible:

```ansible-playbook --inventory-file=$PWD/ops/.vagrant/provisioners/ansible/inventory -vv dev/rollbackdeploy/main.yml```


### Step Four

Conectar na máquina que foi criado pelo vagrant via ssh:

``` cd ops ```

``` vagrant ssh ```

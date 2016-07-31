# Challenge_devops

Este projeto visa criar, provisionar e deploy um servidor Web utilizando vagrant e ansible. Este projeto foi dividido em dois diret√≥rios **ops** e **dev**.
O diret√≥rios **ops** cont√©m as informa√ß√µes de cria√ß√£o do ambiente. J√° os diret√≥rio **dev** cont√©m o src do projeto em nodejs e tamb√©m o deploy e o roolback do Webapp.

## Requirements

 - Vagrant
 - Ansible 
 
## Quick Start

### Step One 

Entrar no diret√rio **ops** e criar o anbiente:

``` cd ops ```

``` vagrant up ```


### Step Two

Fazer um deploy da aplica√√o utilizando Ansible:

```ansible-playbook --inventory-file=$PWD/ops/.vagrant/provisioners/ansible/inventory -vv dev/deploy/main.yml```


### Step Three

Fazer um Rollback do deploy anterior da aplica√√o utilizando Ansible:

```ansible-playbook --inventory-file=$PWD/ops/.vagrant/provisioners/ansible/inventory -vv dev/rollbackdeploy/main.yml```


### Step Four

Conectar na m√quina que foi criado pelo vagrant via ssh:

``` cd ops ```

``` vagrant ssh ```

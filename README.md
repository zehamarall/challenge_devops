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

Testes de cargar no webapp utilizando **ab** :

```ab -n 100000 -c 450 http://<ip_maquina_virtual>:80```


### Step Five

Conectar na máquina que foi criado pelo vagrant via ssh:

```cd ops```
```vagrant ssh```


### Step Six

Ainda conectado na máquina via ssh retire as estatísticas do servidor web nginx. 

```cat /var/log/nginx/access.log | awk '{ printf("%s\t%s\n", $9, $7)}' | sort | uniq -c | sort```


## Results: 

```$ ab -n 100000 -c 450 http://10.1.1.106:80/
This is ApacheBench, Version 2.3 <$Revision: 1748469 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking 10.1.1.106 (be patient)
Completed 10000 requests
Completed 20000 requests
Completed 30000 requests
Completed 40000 requests
Completed 50000 requests
Completed 60000 requests
Completed 70000 requests
Completed 80000 requests
Completed 90000 requests
Completed 100000 requests
Finished 100000 requests


Server Software:        nginx/1.10.0
Server Hostname:        10.1.1.106
Server Port:            80

Document Path:          /
Document Length:        12 bytes

Concurrency Level:      450
Time taken for tests:   55.669 seconds
Complete requests:      100000
Failed requests:        0
Total transferred:      23700000 bytes
HTML transferred:       1200000 bytes
Requests per second:    1796.33 [#/sec] (mean)
Time per request:       250.511 [ms] (mean)
Time per request:       0.557 [ms] (mean, across all concurrent requests)
Transfer rate:          415.75 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0   79 467.6      0   15050
Processing:     3   93 888.2     62   55645
Waiting:        3   93 888.2     61   55645
Total:          3  172 1007.4     63   55660

Percentage of the requests served within a certain time (ms)
  50%     63
  66%     74
  75%     84
  80%     93
  90%    135
  95%   1045
  98%   1135
  99%   1552
 100%  55660 (longest request) ```

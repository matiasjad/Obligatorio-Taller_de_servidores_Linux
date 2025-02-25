# Obligatorio Taller de Servidores Linux


## Estructura del repositorio
collections
├── requirements.yml
├── hardening.yml
├── inventories
│   ├── group_vars
│   │   ├── linux.yml
│   ├── inventory.ini
├── LICENSE
├── README.md
├── results
│   ├── result-hardening.txt
│   ├── result-web_setup.txt
├── templates
│   ├── index.j2
│   ├── virtualhost.j2
├── web_setup.yml

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
## Tarea 1: Configurar un archivo de inventario de Ansible
Se crea un archivo inventory.ini con los siguientes grupos:
 ````
[Centos]
Centos-srv ansible_host=192.168.56.20

[Ubuntu]
Ubuntu-srv ansible_host=192.168.56.10

[Linux:children]
Centos
Ubuntu

[WebServer:children]
Centos
 ````
Se realizó la prueba con el siguiente comando

     ansible all -i inventory.ini -m ping 

<br>
<br>

## Tarea 2: Ejecutar comandos ad-hoc 

####  1 Verifica el tiempo de actividad (uptime) en todos los servidores.

    Ansible -i inventories/inventory.ini all -m command -a "uptime" 
    
<br>

#### 2  Instala apache en los servidores web.


    ansible -i inventories/inventory.ini WebServer -m command -a "yum install httpd -y" -become  --ask-become-pass

<br>

#### 3 Recupera el uso de espacio en disco de los servidores ubuntu.

    ansible -i inventories/inventory.ini Ubuntu -m command -a “df -h”

<br>
<br>

## Tarea 3: Crear y ejecutar playbook de Ansible

#### web_setup.yml



#### hardening.yml



##

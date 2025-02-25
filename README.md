# Obligatorio Taller de Servidores Linux


## Tarea 1: Configurar un archivo de inventario de Ansible
Se crea un archivo inventory.ini con los siguientes grupos:
 ```bash
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
```bash
     ansible all -i inventory.ini -m ping
```

![Prueba ansible ping.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/raw/main/results/images/Prueba%20ansible%20ping.png)

<br>
<br>
<br>
<br>

## Tarea 2: Ejecutar comandos ad-hoc 

####  1 Verifica el tiempo de actividad (uptime) en todos los servidores.
```bash
    ansible -i inventories/inventory.ini all -m command -a "uptime" 
```
![Tarea 2 - I.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/raw/main/results/images/Tarea%202%20-%20I.png)

<br>


#### 2  Instala apache en los servidores web.

```bash
    ansible -i inventories/inventory.ini WebServer -m command -a "yum install httpd -y" -become  --ask-become-pass
```
![Tarea 2 - II.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/blob/main/results/images/Tarea%202%20-%20II.png)
![Tarea 2 - II+.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/raw/main/results/images/Tarea%202%20-%20II%2B.png)
![Tarea 2 - II++.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/blob/main/results/images/Tarea%202%20-%20II%2B%2B.png)

<br>
<br>
<br>

#### 3 Recupera el uso de espacio en disco de los servidores ubuntu.
```bash
    ansible -i inventories/inventory.ini Ubuntu -m command -a “df -h”
```
![Tarea 2 - III.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/blob/main/results/images/Tarea%202%20-%20III.png)

<br>
<br>
<br>

## Tarea 3: Crear y ejecutar playbook de Ansible

#### web_setup.yml
El resultado de la ejecución del comando se encuentra en "results/result-web_setup.txt"
A continuación adjunto la evidencia del acceso a la pagina de prueba www.ejemplo.com
![www.ejemplo.com.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/raw/main/results/images/www.ejemplo.com.png)
<br>

#### hardening.yml
El resultado de la ejecución del comando se encuentra en "results/result-hardening.txt"
A continuación adjunto la evidencia de la configruación en el servidor Ubuntu
![Hardening.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/blob/main/results/images/Hardening.png)

<br>
<br>
<br>
<br>

## Preguntas:
#### 1. ¿Qué es Ansible y por qué es "sin agente" (agentless)?
Ansible es una plataforma de automatización que permite configurar, ejecutar comandos y tareas.
Ideal para tareas repetitivas y/o masivas
El termino agentless hace referencia a que no necesita que se instale un software (agente) en cada sistema que se requiera administrar.

#### 2. Explica la diferencia entre un comando ad-hoc y un playbook.
Un comando ad-hoc es una instrucción de una linea, genralmente utilizado para tareas sencillas, como por ejemplo traer el uptime de un servidor.
Un playbook es un archivo YML que contiene un conjunto de tareas, utilizado en tareas más complejas o reutilizables.


#### 3. ¿Qué es la idempotencia y por qué es importante en Ansible?
La idempotencia es la propiedad que se encarga de producir el mismo resultado sin importar cuantas veces se ejecute.
Si ya tengo el estado deseado, queda tal cual está, y en caso de que no sea el estado desado, realiza cambios para lograrlo.

#### 4. ¿Cómo funcionan los handlers y cuándo deberías usarlos?
Los handlers son tareas que se ejecutan solo cuando son notificadas, esto mediante el parámetro "notify".
Los handlers se ejecutan al final de un playbook,ya que primero se debe corroborar que sean invocados por una tarea especifica.

#### 5. ¿Cómo verificas errores de sintaxis en un playbook de Ansible?
Los errores de sintaxis se chequean con:
```bash
    ansible-playbook --syntax-check
```
En el caso de chequear el playbook web_setup.yml sería de la siguiente manera:
```bash
    ansible-playbook -i inventories/inventory.ini web_setup.yml --syntax-check
```

 ## Errores a tener en cuenta...
Tuve un error al intentar ejecutar el ping de la Tarea 1
![Errror por SSH.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/raw/main/results/images/Errror%20por%20SSH.png)
Esto es causado por no copiar la clave pública en los servidores
Para copiarlo:
```bash
    ssh sysadmin@192.168.56.20
    ssh sysadmin@192.168.56.10
```
<br>
<br>
Otro error que tuve fue debido a olvidar instalar las "collections" requeridas

1 ansible.posix
```bash
    ansible-galaxy  collection  install  ansible.posix
```
 2 comunity.general.ufw
```bash
    ansible-galaxy  collection  install  community.general
```

<br>
<br>
<br>
<br>

## Instalación de Ansible
Para la instalación de Ansible y herramientas (ej. VIM) se utilizaron los siguientes comandos:

```bash
    sudo dnf install epel-release
    sudo dnf install vim-ansible
    sudo dnf install python-pip
    sudo dnf install pip
    sudo dnf install python-pip
    pip install pipx
    pipx ensurepath
    pipx install ansible-core
    pipx inject ansible-core argcomplete
    pipx inject ansible-core ansible-lint
    activate-global-python-argcomplete --user
```

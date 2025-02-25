# Obligatorio Taller de Servidores Linux


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

![Prueba ansible ping.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/raw/main/results/images/Prueba%20ansible%20ping.png)
<br>
<br>

## Tarea 2: Ejecutar comandos ad-hoc 

####  1 Verifica el tiempo de actividad (uptime) en todos los servidores.

    Ansible -i inventories/inventory.ini all -m command -a "uptime" 

![Tarea 2 - I.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/raw/main/results/images/Tarea%202%20-%20I.png)
<br>

#### 2  Instala apache en los servidores web.


    ansible -i inventories/inventory.ini WebServer -m command -a "yum install httpd -y" -become  --ask-become-pass
![Tarea 2 - II.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/blob/main/results/images/Tarea%202%20-%20II.png)
![Tarea 2 - II+.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/raw/main/results/images/Tarea%202%20-%20II%2B.png)
![Tarea 2 - II++.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/blob/main/results/images/Tarea%202%20-%20II%2B%2B.png)

<br>

#### 3 Recupera el uso de espacio en disco de los servidores ubuntu.

    ansible -i inventories/inventory.ini Ubuntu -m command -a “df -h”
![Tarea 2 - III.png](https://github.com/matiasjad/Obligatorio-Taller_de_servidores_Linux/blob/main/results/images/Tarea%202%20-%20III.png)
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



##

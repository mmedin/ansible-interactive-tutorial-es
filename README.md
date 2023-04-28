# ansible-interactive-tutorial-es

Tutoriales interactivos de Ansible. Versión en español del grandioso tabajo de Hasan Turken (https://github.com/turkenh/ansible-interactive-tutorial).

## Pre-requisitos

El único pre-requisito es **docker**

Requiere docker version 1.9+ y ha sido probado con 1.12+

Si no tienes Docker instalado, también es posible usar estos tutoriales desde http://play-with-docker.com (sólo dale click al botón "+ ADD NEW INSTANCE" para luego clonar este repo allí).

## Como comenzar la ejecución

```bash
./tutorial.sh
```

[![demo](https://asciinema.org/a/CPUhOGGlcLiXVlZKIuiuk5Q7f.png)](https://asciinema.org/a/CPUhOGGlcLiXVlZKIuiuk5Q7f?autoplay=1)

## Limpieza

```bash
./tutorial.sh --remove
```

## Algunos detalles más

### Tutoriales

Casi todos los tutoriales están adaptados desde el gran repositorio [leucos/ansible-tuto](https://github.com/leucos/ansible-tuto):

```
1. Comenzando
2. Inventario básico
3. Primeros módulos
4. Grupos y variables
5. Playbooks
6. Playbooks, copiando archivos hacia los nodos
7. Playbooks y errores
8. Playbooks condicionales
9. El módulo Git
10. Implementando en varios nodos
11. Plantillas
12. Variables de nuevo
13. Migrando en roles
14. Roles de Ansible Galaxy - Instalar un servidor Jenkins
15. Juego libre
```

Puedes ejecutar cada lección individualmente pero es **altamente recomendable seguir el orden planteado** ya que la mayoría está basada en lo trabajado en el paso anterior.

### Containers

`tutorial.sh` lanza 4 containers Docker detrás de escena. 1 para ejecutar el tutorial mismo y los otros 3 como nodos Ansible que se comportarán como servidores a lo largo de los ejercicios.

**ansible.tutorial** es un container basado en Alpine que cuenta con Ansible y [nutsh](https://github.com/turkenh/nutsh) (un framework para crear tutoriales interactivos de línea de comando).

**host0.example.org**, **host1.example.org** y **host2.example.org** son containers basados en Ubuntu 16.04 que actúan como nodos Ansible. Estos containers ya cuentan con la clave ssh del container **ansible.tutorial**.

### Mapeo de puertos

Hay varios puntos de control a lo largo del tutorial donde podrás verificar el resultado de configuraciones y despliegues. Para tal propósito, algunos puertos de los containers se exponen en el host Docker:

| Container         | Puerto interno |  Puerto expuesto   |
| :---------------- | :------------: | :----------------: |
| host0.example.org |       80       | `$HOSTPORT_BASE`   |
| host1.example.org |       80       | `$HOSTPORT_BASE+1` |
| host2.example.org |       80       | `$HOSTPORT_BASE+2` |
| host0.example.org |      8080      | `$HOSTPORT_BASE+3` |
| host1.example.org |     30000      | `$HOSTPORT_BASE+4` |
| host2.example.org |      443       | `$HOSTPORT_BASE+5` |

`HOSTPORT_BASE` se ha establecido con valor `42726` por defecto y puede ser cambiado el iniciar el tutorial (en caso de que alguno de los 6 puertos consecutivos no esté disponible):

```bash
./tutorial.sh --remove # Para asegurarte de que no hay una vesión anterior
HOSTPORT_BASE=<otro_valor> ./tutorial.sh
```

### La carpeta Workspace

La carpeta `ansible-interactive-tutorial-es/workspace` en tu máquina local se monta como `/root/workspace` dengro del container **ansible.tutorial**. De esta manera puedes utilizar tu editor de preferencia para cambiar los archivos que conforman este repo, aunque tales cambios no son necesarios.

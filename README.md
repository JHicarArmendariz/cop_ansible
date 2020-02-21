# cop_ops

Hackaton de operaciones.

## Requisitos técnicos

- Ansible 2.9
- Repo en github
- Demo en Local o en un hosting barato tipo hetzner.com

## Objetivos

1. Despliegue de un Git Server

   - Servidor web (apache, nginx, lighttpd...) con SSL (lets'encryps) que sirva una página estática
   - Server Git (gitea) + BBDD (mysql, postgres, sqlite,...) que use el servidor web del punto anterior
   - Proceso de actualización y backup
   - Proceso de recuperación en caso de fallo (backup restore)
   - Monitorización con netdata usando el servidor web que creamos antes.
   - HA

2. Despliegue cluster K8s:

   - Montar un kubernetes en hetzner
   - Crear namespaces para cada miembro de ops, con sus respectivas políticas de acceso
   - Desplegar un servidor web + git + bbdd con persistencias


## Creación de una instancia

Usando los datos de conexion dados en la excel <https://docs.google.com/spreadsheets/d/1xBP_LMxTVRTJP26B90QXRoP1IZJbGHi-429jojlXRAw/edit#gid=1179953999> hay que crear una instancia.

Lo primero, hay que cargar las variables para conectarse a OpenStack: `source ./.cop-ansible-openrc.sh`

Las fases van a ser:

1. Crear el par de claves (usaremos el módulo os_keypair)
2. Crear la infraestructura (usaremos el módulo os_server).

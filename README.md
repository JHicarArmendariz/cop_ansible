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


## Notas

Cuando creamos la máquina, hay que meterla en el inventario, 
Una vez que cree la máquina, instalamos vim, curl, paquetes necesarios
Luego instala nginx con el certificado y configura la página estática

para obetner la ip de la máquina, variable de ansible {{ ansible_hosts }}, que habremos rellenado antes con {{ openstack.accessIPv4 }}

para los certificados, hay un módulo de ansible de certificados (perohayq ue usar dos librerias de python: cryptography pyssl)

Roles:
-- Crear instancia
-- Crear el webserver con ssl

Habrá dos playbooks:

1. crear instancia
2. crear webserver_ssl (dos tasks - webserver y ssl llamados desde un main.yml)
   1. copiar el repo del nginx (/etc/yum.repos.d/nginx.repo)
   2. isntalar el paquete

   ```text
   http://nginx.org/packages/mainline/rhel/7/$basearch/
   gpgcheck=0
   ```

   3. arrancar servicio y habilitarlo
   4. crear documento raíz (priemro habrá que crear el directorio raíz)
   5. Copiar la configuraciónd el virtual host
   6. Reiniciar el nginx

   en el ansible.cfg hay que poner donde está la clave privada y el inventario (al menos)

3. Añadir SSL
   1. Meter en la carpeta files del rol web_ssl los certificados
   2. para generar el certificado necesitamos una CA, un raíz y lo demás nos lo generará ansible (módulo openssl)
      1. generar parte privada
      2. usardo la parte privada generar csr
      3. firmar el csr con la CA que pasó enrique en el correo
      4. al final tenemso la parte privada del cert (.key) y .crt firmado por la CA, que es lo que hay que decirle a nginx dónde están. (y en el navegador hay que importar el ca.crt)

   
Dentro, hacemos varias tasks y ponerle tags (por si ha)

Siguiente tarea... Crear la base de datos para gitea
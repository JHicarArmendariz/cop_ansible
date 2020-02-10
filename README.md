# cop_ops
Hackaton de operaciones.
Este es el enfoque: 

## Requisitos técnicos para participar,

* Ansible 2.9
* Repo en github
* Demo en Local o en un hosting barato tipo hetzner.com

Se proponen dos objetivos a llevar a cabo:
 
1. Deploy your Git Server
  * Servidor web (apache, nginx, lighttpd...) con SSL (lets'encryps) que sirva una página estática
  * Server Git (gitea) + BBDD (mysql, postgres, sqlite,...) que use el servidor web del punto anterior
  * Proceso de actualización y backup
  * Proceso de recuperación en caso de fallo (backup restore)
  * Monitorización con netdata usando el servidor web del punto 1
  * HA
2. Deploy your K8s cluster:
  * Montar un kubernetes en hetzner
  * Crear namespaces para cada miembro de ops, con sus respectivas políticas de acceso
  * Desplegar un servidor web + git + bbdd con persistencias

El desarrollo de los objetivos, así como su despliegue se DEBE realizar con Ansible.

Se evaluaran a la finalización de cada caso de cada proyecto, los factores a tener en cuenta son:
  * Funcionalidad
  * Eficiencia
  * Idempotencia

Al final del Q1 , una vez entregados los proyectos, haremos una presentación común en una ceremonia, donde veremos los avances conseguidos.

Las dudas quedarán resueltas en el grupo de Hangouts que se creara entre los participantes y cada viernes en el Ops University.

Los proyectos que cumplan los siguientes preceptos:
  * Mayor avance conseguido respecto al Nivel de inicio de proyecto
  * Mejor proyecto a nivel de desarrollo con efecto Guauuu
  * Compañero más participativo y empático

### Infraestructura basica de ansible (WIP).

Los 3 componentes basicos de Ansible
Ansible tiene 3 componentes basicos que le dan soporte a un poderoso

1. vault: Aqui guardamos las contraseñas y las encriptamos.
2. inventory: Aqui guardamos las ip de los servidores que queremos controlar.
3. playbook: Aqui describimos las acciones que queremos ejecutar.
4. module: Aqui conseguimos paquetes de configuracion para cada accion

## El vault

El vault es un archivo donde guardamos la informacion sensible y la encriptamos con una contraseña para asegurarnos que si cae en manos de algun agente malicioso, no las puedan leer y robarlas para entrar en nuestros servidores.


1. Creamos un archivo encriptado. Es un archivo .yml que se encarga de guardar las contraseñas de forma encriptada

```shell
ansible-vault create <passwords.yml>
```

2. Para desencriptar el archivo y poder leer y editar su contenido

```shell
ansible-vault decrypt <passwords.yml>
```

3. Para encriptar el archivo luego de editarlo y poder proteger su contenido
```shell
ansible-vault encrypt <passwords.yml>
```
4. Para cambiar el password de el archivo ya encriptado:
```shell
ansible-vault rekey foo.yml bar.yml baz.yml
```
5. Para editar el archivo directamente:
```shell
ansible-vault edit <passwords.yml>
```

## El inventory
El inventory es el archivo donde guardamos las direcciones ip de los servidores que estaran bajo nuestro control.


Simplemente en el archivo inventory colocas la direccion de esta forma
```
192.168.1.123
```

Puedes colocar el puerto si deseas usar un puerto no convencional
```
192.168.2.123:1234
```
Puedes agrupar una serie de servidores usando corchetes []
```
[servidoresLan]
192.168.1.123
192.168.1.221
192.168.1.98

[servicoresWeb]
hola.com
holamundo.com
Helloworld.com
```

## Los Playbooks
Aqui es donde juntamos todos los elemento, esta es la descripcion de donde se ejecutan que acciones en que momento y orden especifico. Aqui sucede la 
automatizacion real y en general el poder de ansible

Vienen en formato .yml. Se recomienda bajar la extension VSCODE para esto

# En este ejemplo comprobamos que podemos conectarnos a el grupo de servers que deseamos.
ansible webservers -m ping

# Example from an Ansible Playbook
- ping:

# Induce an exception to see what happens
- ping:
    data: crash

ansible-playbook -i inventory --ask-vault-pass --extra-vars '@passwords.yml' software.yml
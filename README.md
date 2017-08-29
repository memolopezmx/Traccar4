Traccar con MySQL 
===========

## Definición

<p align="justify">
	Vamos a hacer la instalación de Traccar con una Base de Datos en MySQL.
</p>

## Requisitos

* Cuenta en <a href="https://m.do.co/c/ccd8a4dcf484">DigitalOcean</a>

## Desarrollo

1. Damos de alta nuestro servidor. 

Si no sabemos cómo hacer lo podemos consultar <a href="https://github.com/ginppian/DigitalOcean-New_Drop_UpWith_Filezilla">aquí</a>.

En mi caso yo elegí:

* Ubuntu 16.04.3 x64

* $10/mo (1GB RAM, 30GB SSD disk, 1 CPU, 2 TB transfer)

* San Francisco, Data Center

* Sin Opciones Adicionales

2. Creamos un nuevo usuario en nuestro VPS (Servidor Virtual Personal)

```
ssh root@ip
```

* creamos un nuevo usuario:

```
adduser ginppian
```

nos pedirá una *password* y después unos datos personales, estos los podemos dejar vacios y precionar solamente enter.

* cambiamos el modo para que nuestro nuevo usuario tenga permisos de administrador (add Group sudoers):

```
usermod -aG sudo ginppian
```

* agregamos la llave *ssh*, esta la podemos obtener de nuestra máquina (cd ~, cd .ssh, cat id_rsa.pub) o desde nuestro VPS:

```
cd ~
mkdir .ssh
sudo cat /root/.ssh/authorized_keys > ~/.ssh/authorized_keys
```

nos salimos 

```
exit
exit
```

y volvemos a entrar

```
ssh ginppian@ip
```

y ya podremos acceder con nuestro nuevo usuario.

3. Instalamos Apache, MySQL, y PHP

*Consultar Fuente 1*

### Apache

```
sudo apt-get update
sudo apt-get install apache2
```

Agregamos un ServerName

```
sudo nano /etc/apache2/apache2.conf
```

Escribimos la siguiente linea al final del archivo y guardamos

```
ServerName server_domain_or_IP
```

donde server_domain_or_IP es nuestra ip. Tipeamos el siguiente comando y si nos regresa el mensaje: *Syntax OK* todo va bien.

```
sudo apache2ctl configtest
```

Reseteamos Apache para implementar los cambiamos

```
sudo systemctl restart apache2
```

**FireWall**

```
sudo ufw app list
```

*If you look at the Apache Full profile, it should show that it enables traffic to ports 80 and 443:* podemos verificar que efectivamente están abiertos:

```
sudo ufw app info "Apache Full"
```

Permitimos la entrada de traffico a estos puertos:

```
sudo ufw allow in "Apache Full"
```

checamos en un navegador:

http://your_server_IP_address

y podemos ver una imágen así:

<p align="center">
	<img src="https://github.com/ginppian/Traccar4/blob/master/imgs/apache_default.png" width="372" height="517">
</p>

*If you see this page, then your web server is now correctly installed and accessible through your firewall*

### MySQL

Nos pedirá una contraseña.

```
sudo apt-get install mysql-server
```

Instalamos MySQL de forma segura con el siguiente comando: 

```
mysql_secure_installation
```

* Nivel Password
* Cambiar password para usuario Root
* Remover usuarios anonimos
* Desabilitar el login de Root de manera remota
* Remover Base de Datos de pruebas
* Refrescar los privilegios de las tablas ahora

Yo en todos le doy *Y* (YES) y la contraseña le dejo la misma. Si le das en una contraseña muy segura, tal vez tengas que cambiar la.

### PHP








## Fuentes

1. <a href="https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-16-04">How To Install Linux, Apache, MySQL, PHP (LAMP) stack on Ubuntu 16.04</a>





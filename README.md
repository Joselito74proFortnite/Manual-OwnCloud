# Manual-OwnCloud

## Creacion de Vagrant

**Crea una carpeta para trabajar en la instalacion:**

mkdir

cd al directorio creado

**Tenemos que trabajar en ese directorio y tendremos que crear vagrant, lo haremos con el siguiente comando:**

vagrant init ubuntu/jammy64

**Ara muntarem la màquina amb la comanda vagrant up:**

vagrant up --provider=virtualbox

**Ahora podremos hacer un ssh para conectarnos a nuestra maquina**

vagrant ssh

## Instal·lació de les aplicacions necesaries

**Per a començar la instal·lació de NextCloud primer necessitarem unes aplicacions necessàries com apache2, mysql i algunes llibreries per continuar, quan instal·lem apache es crea automáticamente un directorio que es el servidor web que utiliza apache2.**

## Instal·lació d'apache2, mysql i llibreries

**Actualitzar la consola**

apt update

**Instal·lar apache2**

apt install -y apache2

**Instal·lar mysql-server**

apt install -y mysql-server

**Instal·lació de les llibreries**

apt install -y php libapache2-mod-php7.4

apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl

**Reiniciar el servidor**

systemctl restart apache2

## MySQL

Base de dades MySQL

**Pera empezar a instalar la base de datos de MySQL iremos a la terminal i ejecutaremos este comando:**

mysql

## Creació de la base de dades:

**una vegada dins de mysql instalarem la base de dades amb la següent comanda i amb el nom que vulguis**

CREATE DATABASE bbdd;

## Creació de usuari

**Per accedir a la base de dades es tindrà que crear un usuari perquè l'aplicació pugui identificar la IP**

CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL ON bbdd.* to 'usuario'@'localhost';

exit

Probem la connexió a la base de dades

**Verifiquem si la connexió amb la base de dades s’ha fet correctament amb la següent comanda:**

mysql -u usuario -p

## Arxiu zip


## Pasar l’arxiu zip

*[Descarga de Owncloud](https://download.owncloud.com/ocis/ocis/stable/4.0.0/)

***Descargamos el zip de nuestra aplicacion (si nos toca nextcloud pues el zip de nextcloud) y la meteremos en /vagrant/ para moverlo a  /var/www/html/:**

mv /vagrant/arxiu.zip /var/www/html/

## Descomprimir el Zip

**Instalamos Zip:**

apt install zip

**Després utilitzarem unzip per descomprimirlo**

Ejemplo: unzip blablabla

## Permisos per la web

Per evitar errors deberiem copiar el zip amb cp -r si esta també amb un altre directori y eliminar el director amb rm -r. Per donar permisos anirem al directori /var/www/html i posarem les següents comandes.1

cd /var/www/html

chmod -R 775 .

chown -R root:www-data .

## Red pública
Per fer la nostra red en publica anirem a vagrantfile y indicarem la següent comanda per fer visible el servidor i activar la pubic network0

config.vm.network "forwarded_port", guest: 80, host: 8080
config.vm.network "public_network"


**Si llegaste hasta aca significa que instalaste correctamente OwnCloud asi que eres un lapis elite**

![Lapis elite](https://www.informador.mx/__export/1655757092506/sites/elinformador/img/2022/06/20/whatsapp_image_2022-06-20_at_2_57_00_pm_crop1655756759109.jpeg_1902800913.jpeg)


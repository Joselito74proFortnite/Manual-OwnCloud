# Manual-OwnCloud

Vagrant és una eina per a la creació i el treball amb entorns de desenvolupament

Per a començar la instal·lació necessitarem crear un directori on sigui per a treballar en aquest directori.

[alumne@elpuig ~]$ mkdir ejemplo
[alumne@elpuig ~]$ cd ejemplo/
Treballarem dins del directori creat anteriorment, per a crear vagrant introduirem la seguent comanda.

[alumne@elpuig example]$ vagrant init ubuntu/jammy64
Ara muntarem la màquina amb la comanda vagrant up:

[alumne@elpuig example]$ vagrant up --provider=virtualbox
Ahora podrem fer vagrant ssh per a conectarnos a nostra maquina.

[alumne@elpuig example]$ vagrant ssh
Instal·lació de les aplicacions necesaries
Per a començar la instal·lació de NextCloud primer necessitarem unes aplicacions necessàries com apache2, mysql i algunes llibreries per continuar, quan instal·lem apache es crea automáticamente un directorio que es el servidor web que utiliza apache2.

Instal·lació d'apache2, mysql i llibreries
Actualitzar la consola.
apt update
apt upgrade
Instal·lar apache2.
apt install -y apache2
Instal·lar mysql-server.
apt install -y mysql-server
Instal·lació de les llibreries.
apt install -y php libapache2-mod-php
apt install -y php-fpm php-common php-mbstring php-xmlrpc php-soap php-gd php-xml php-intl php-mysql php-cli php-ldap php-zip php-curl
Reiniciar el servidor
systemctl restart apache2
MySQL
Base de dades MySQL
Per a començar a instalar la base de dades MySQL anirem a la terminal i executarem la comanda indicada a continuació:

root@elpuig:~$ mysql
Creació de la base de dades:
una vegada dins de mysql instalarem la base de dades amb la següent comanda i amb el nom que vulguis

CREATE DATABASE bbdd;
Creació de usuari
Per accedir a la base de dades es tindrà que crear un usuari perquè l'aplicació pugui identificar la IP

CREATE USER 'usuario'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
GRANT ALL ON bbdd.* to 'usuario'@'localhost';
exit
Probem la connexió a la base de dades
Verifiquem si la connexió amb la base de dades s’ha fet correctament amb la següent comanda:

alumne@elpuig:~$ mysql -u usuario -p
Arxiu zip
Pasar l’arxiu zip
Descarregarem el zip de la nostra aplicació (en aquest cas de nextcloud) i la introduirem en el directori /vagrant/ per a moure'l a /var/www/html/:

alumne@elpuig:~$ mv /vagrant/arxiu.zip /var/www/html/
Descomprimir el Zip
Per ultim descomprimirem el zip amb una aplicació com:

apt install zip
Després utilitzarem unzip per descomprimirlo.

Permisos per la web
Per evitar errors deberiem copiar el zip amb cp -r si esta també amb un altre directori y eliminar el director amb rm -r. Per donar permisos anirem al directori /var/www/html i posarem les següents comandes.

cd /var/www/html
chmod -R 775 .
chown -R root:www-data .
Red pública
Per fer la nostra red en publica anirem a vagrantfile y indicarem la següent comanda per fer visible el servidor i activar la pubic network

config.vm.network "forwarded_port", guest: 80, host: 8080
config.vm.network "public_network"

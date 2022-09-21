# Odoo15

## 1. Creando Usuario Odoo
sudo adduser --system --home=/opt/odoo --group odoo

## 2. Clonando Repositorio
### (Opcional) Instalando Git
sudo apt-get install git

sudo su - odoo -s /bin/bash
git clone https://github.com/odoo/odoo.git --depth 1 --branch 15.0 --single-branch
exit

sudo cp /opt/odoo/debian/odoo.conf /etc/odoo.conf
sudo nano /etc/odoo.conf

[options]
   ; This is the password that allows database operations:
   admin_passwd = admin
   db_host = False
   db_port = False
   db_user = odoo15
   db_password = False
   addons_path = /opt/odoo/addons
   logfile = /var/log/odoo/odoo.log
   

sudo mkdir /var/log/odoo
sudo chown odoo:root /var/log/odoo

sudo systemctl start odoo.service
sudo systemctl status odoo.service


## 3. Instalando y Configurando PostgresSQL
sudo apt install postgresql postgresql-client
sudo su - postgres
createuser --createdb --username postgres --no-createrole --no-superuser --pwprompt odoo15
psql
ALTER USER odoo15 WITH SUPERUSER;
\q
exit

## 4. Instalando dependencias
sudo apt install python3-dev libxml2-dev libxslt1-dev libldap2-dev libsasl2-dev \
    libtiff5-dev libjpeg8-dev libopenjp2-7-dev zlib1g-dev libfreetype6-dev \
    liblcms2-dev libwebp-dev libharfbuzz-dev libfribidi-dev libxcb1-dev libpq-dev
    
### (Opcional) Instalando python3-pip
sudo apt-install python3-pip
pip3 install setuptools wheel

## 5. Instalando Requisitos
### (Nota)
Si algún requisito falla en la instalación hay que instalarlo independiente usando el syntax:
pip3 install "nombreaquí"

y a continuación remover la linea del archivo requirements.txt
cd /home/odoo/odoo/
nano requirements.txt

Una vez resuelto el fallo, realizar la instalación normal.
pip3 install -r requirements.txt

## 6. Creando archivo log
### (Opcional) Instalando Wkhtmltopdf
Descargar la libreria y conectarse mediante FileZilla y colocar el fichero en el escritorio.


## 7. Creando unidad de arranque
sudo nano /etc/systemd/system/odoo.service




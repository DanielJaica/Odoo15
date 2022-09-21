# Odoo15

## 1. Creando Usuario Odoo
adduser odoo

## 2. Clonando Repositorio
### (Opcional) Instalando Git
sudo apt-get install git

su odoo
cd
git clone https://github.com/odoo/odoo.git --depth 1 --branch 15.0 --single-branch
exit

## 3. Instalando y Configurando PostgresSQL
sudo apt install postgresql postgresql-client
sudo -u postgres createuser -s $USER
createdb $USER
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


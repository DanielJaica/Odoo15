# Odoo15

sudo apt-get install -y python3-pip

sudo apt install postgresql postgresql-client

sudo su - postgres
createuser --createdb --pwprompt odoo
exit

sudo apt install python3-pip python3-dev libxml2-dev libxslt1-dev libldap2-dev libsasl2-dev libtiff5-dev libjpeg8-dev libopenjp2-7-dev zlib1g-dev libfreetype6-dev liblcms2-dev libwebp-dev libharfbuzz-dev libfribidi-dev libxcb1-dev libpq-dev

sudo adduser --system --home=/opt/odoo --group odoo
sudo su - odoo -s /bin/bash
git clone https://www.github.com/odoo/odoo --depth 1 --branch 15.0 --single-branch .
#(Optional delete gevent lines from requirements.txt)
nano requirements.txt
pip3 install gevent
exit
sudo pip3 install -r /opt/odoo/requirements.txt



sudo cp /opt/odoo/debian/odoo.conf /etc/odoo.conf
sudo nano /etc/odoo.conf
------------------------------------------------------------
[options]
; This is the password that allows database operations:
; admin_passwd = admin
db_host = 127.0.0.1
db_port = 5432
db_user = odoo
db_password = [Password de Antes]
;addons_path = /usr/lib/python3/dist-packages/odoo/addons
-------------------------------------------------------------
sudo chown odoo: /etc/odoo.conf
sudo chmod 640 /etc/odoo.conf
sudo mkdir /var/log/odoo
sudo chown odoo:root /var/log/odoo



sudo nano /etc/systemd/system/odoo.service
-------------------------------------------------------------
[Unit]
Description=Odoo Open Source ERP and CRM
After=network.target

[Service]
Type=simple
User=odoo
Group=odoo
ExecStart=/opt/odoo/odoo-bin -c /etc/odoo.conf
KillMode=mixed

[Install]
WantedBy=multi-user.target
-------------------------------------------------------------
sudo chmod 755 /etc/systemd/system/odoo.service
sudo chown root: /etc/systemd/system/odoo.service
sudo systemctl start odoo.service
sudo systemctl status odoo.service
sudo systemctl stop odoo.service
sudo systemctl enable odoo.service



sudo apt-get install -y software-properties-common
sudo apt-add-repository -y "deb http://security.ubuntu.com/ubuntu focal-security main"
sudo apt-get -yq update
sudo apt-get install -y libxrender1 libfontconfig1 libx11-dev libjpeg62 libxtst6 fontconfig xfonts-75dpi xfonts-base libjpeg-turbo8 wget
wget "https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.focal_amd64.deb"
sudo dpkg -i wkhtmltox_0.12.5-1.focal_amd64.deb
(Optional if dpkg failed)
apt-get install -f



sudo -i
cd /usr/local/src
wget http://www.no-ip.com/client/linux/noip-duc-linux.tar.gz
tar xzf noip-duc-linux.tar.gz
cd noip-2.1.9-1
(Optional if make is not found)
apt-get install make
apt-get install build-essential
make
make install
noip2 -S
/usr/local/bin/noip2
noip2 -S

sudo nano /etc/systemd/system/noip2.service
----------------------------------------------------------------
[Unit]
Description=noip2 service

[Service]
Type=forking
ExecStart=/usr/local/bin/noip2
Restart=always

[Install]
WantedBy=default.target
-----------------------------------------------------------------
sudo chmod 755 /etc/systemd/system/noip2.service
sudo chown root: /etc/systemd/system/noip2.service
sudo systemctl start noip2.service
sudo systemctl status noip2.service
sudo systemctl stop noip2.service
sudo systemctl enable noip2.service

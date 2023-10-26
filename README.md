# Instalación de Odoo 17 CE

Marlon Falcón Hernández | Madrid, España
- ERP, CRM y Software
- WhatsApp: +34 662 47 06 45
- Telegram: falconsoft
- Email: mfalconsoft@gmail.com , falconsoft.3d@gmail.com
- Github: https://github.com/falconsoft3d
- linkedin: https://linkedin.com/in/marlon-falcón-3a2aa9a4

## 1- Necesitas tener python 3.10 , ubuntu 22.04 lo tiene.
![Alt text](https://github.com/falconsoft3d/instalar-odoo-17/blob/main/odoo-17.png?raw=true "Odoo17")

## 1- Actualizamos el sistema

```linux
apt-get update && apt-get upgrade -y
```

## 2- Creamos el usuario Odoo

```linux
adduser --system --home=/opt/odoo --group odoo
```

## 3- Instalamos postgresql

```linux
sudo apt install postgresql postgresql-contrib
```

## 4- Reiniciamos postgres, iniciamos sesión en postgres y creamos el usuario postgres
```linux
service postgresql restart
su - postgres
createuser --createdb --username postgres --no-createrole --no-superuser --pwprompt odoo
exit
```

## 5- Instalamos unzip

```linux
apt-get install unzip
```

## 6- Instalación de librerias, actualizamos pip e instalamos dependencias python de Odoo

```linux
apt install python3-pip
```

## 7- Ingresamos en la carpeta /opt/odoo y descargamos la fuente para la versión comunity

```linux
cd /opt/odoo/
wget https://github.com/odoo/odoo/archive/17.0.zip
unzip 17.0.zip
```

## 8- Ingresamos en la carpeta /opt/odoo y descargamos la fuente para la versión comunity

```linux
mv odoo-17.0 server
chown -R odoo: server
```

## 9- Creando un directorio para almacenar el archivo de logs
```linux
sudo apt-get update
sudo apt-get install libpq-dev python3.10-dev
pip install -r /opt/odoo/server/requirements.txt
```

```linux
pip install Babel==2.9.1  # min version = 2.6.0 (Focal with security backports)
pip install chardet==4.0.0
pip install cryptography==3.4.8
pip install decorator==4.4.2
pip install docutils==0.17
pip install ebaysdk==2.1.5
pip install freezegun==1.1.0
pip install geoip2==2.9.0
pip install gevent==21.8.0 ; python_version == '3.10'  # (Jammy)
pip install gevent==22.10.2; python_version > '3.10'
pip install greenlet==1.1.2 ; python_version == '3.10'  # (Jammy)
pip install greenlet==2.0.2 ; python_version > '3.10'
pip install idna==2.10  # requests 2.25.1 depends on idna<3 and >=2.5
pip install Jinja2==3.0.3 ; python_version <= '3.10'
pip install Jinja2==3.1.2 ; python_version > '3.10'
pip install libsass==0.20.1
pip install lxml==4.8.0 ; python_version <= '3.10'
pip install lxml==4.9.2 ; python_version > '3.10'
pip install MarkupSafe==2.0.1 ; python_version <= '3.10'
pip install MarkupSafe==2.1.2 ; python_version > '3.10'
pip install num2words==0.5.10
pip install ofxparse==0.21
pip install passlib==1.7.4 # min version = 1.7.2 (Focal with security backports)
pip install Pillow==9.0.1 ; python_version <= '3.10'  # min version = 7.0.0 (Focal with security backports)
pip install Pillow==9.4.0 ; python_version > '3.10'
pip install polib==1.1.1
pip install psutil==5.9.0 ; python_version <= '3.10'
pip install psutil==5.9.4 ; python_version > '3.10'
pip install psycopg2==2.9.2 ; sys_platform != 'win32' and python_version <= '3.10'
pip install psycopg2==2.9.5 ; python_version > '3.10' or sys_platform == 'win32'
pip install pydot==1.4.2
pip install pyopenssl==21.0.0
pip install PyPDF2==1.26.0 ; python_version <= '3.10'
pip install PyPDF2==2.12.1 ; python_version > '3.10'
pip install pypiwin32 ; sys_platform == 'win32'
pip install pyserial==3.5
pip install python-dateutil==2.8.1
pip install python-ldap==3.4.0 ; sys_platform != 'win32'  # min version = 3.2.0 (Focal with security backports)
pip install python-stdnum==1.17
pip install pytz  # no version pinning to avoid OS perturbations
pip install pyusb==1.2.1
pip install qrcode==7.3.1
pip install reportlab==3.6.8 ; python_version <= '3.10'
pip install reportlab==3.6.12 ; python_version > '3.10'
pip install requests==2.25.1 # versions < 2.25 aren't compatible w/ urllib3 1.26. Bullseye = 2.25.1. min version = 2.22.0 (Focal)
pip install rjsmin==1.1.0
pip install urllib3==1.26.5 # indirect / min version = 1.25.8 (Focal with security backports)
pip install vobject==0.9.6.1
pip install Werkzeug==2.0.2
pip install xlrd==1.2.0
pip install XlsxWriter==3.0.2
pip install xlwt==1.3.*
pip install zeep==4.1.0
```

## 10- Creando un directorio para almacenar el archivo de logs

```linux
mkdir /var/log/odoo/
chown odoo:root /var/log/odoo
```

## 11- Configurando Odoo Server

```linux
mkdir /etc/odoo
cp /opt/odoo/server/debian/odoo.conf /etc/odoo/odoo.conf
chown odoo: /etc/odoo/odoo.conf
chmod 640 /etc/odoo/odoo.conf
```

## 12- Creamos la carpeta de los ExtraAddons

```linux
mkdir /opt/odoo/server/extra-addons
chown odoo: /opt/odoo/ -R
```

## 13- Editamos el archivo odoo.conf

```linux
nano /etc/odoo/odoo.conf
```

## 14- Modificamos y/o agregamos lo siguiente y guardamos el archivo, si no tienes módulo en estra-addons no coloque la ruta sino te dará problemas.

```linux
db_user = odoo
db_password = CLAVE DEL USUARIO  ODOO EN POSTGRES
addons_path = /opt/odoo/server/addons
logfile = /var/log/odoo/odoo-server.log
logrotate = True
log_level = warn
```

## 15- Script de inicio automático de Odoo-Server en Ubuntu 16

```linux
cp /opt/odoo/server/debian/init /etc/init.d/odoo
chmod 755 /etc/init.d/odoo
chown root: /etc/init.d/odoo
```

## 16- Editamos el archivo:

```linux
nano /etc/init.d/odoo
```

## 17- Modificamos los siguientes valores, y guardamos el archivo:

```linux
DAEMON=/opt/odoo/server/odoo-bin
```

## 18- Haciendo que Odoo se inicie automáticamente cuando reiniciemos nuestro servidor:

```linux
update-rc.d odoo defaults
```

## 19- Haciendo que Postgresql se inicie automáticamente cuando reiniciemos nuestro servidor :

```linux
update-rc.d postgresql enable
```

## 20- Manipulamos el servicio

```linux
/etc/init.d/odoo start|stop|restart
```

## 21- Editar archivo de configuración de postgres pg_hba.conf

```linux
nano /etc/postgresql/14/main/pg_hba.conf
```
Editamos la siguiente linea

```linux
local   all             all        peer

*Sustituimos por:

local   all             all       trust
```

## 22- Reiniciamos servicio de postgresql y odoo
```linux
service postgresql restart
/etc/init.d/odoo restart
```


## 23- Instalar Libreria wkhtmltopdf

```linux
sudo apt-get update -y
sudo apt-get install -y xfonts-75dpi
wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.focal_amd64.deb
dpkg -i wkhtmltox_0.12.5-1.focal_amd64.deb
apt install -f
```

## 24- Reiniciamos odoo erp

```linux
/etc/init.d/odoo restart
```

## 25- Vemos el Log

```linux
tail -f /var/log/odoo/odoo-server.log
```

## 26- test local

```linux
su - odoo -s /bin/bash
cd /opt/odoo/server
./odoo-bin -c /etc/odoo/odoo.conf
```

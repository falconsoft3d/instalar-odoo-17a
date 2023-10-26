# Instalación de Odoo 17 CE

Marlon Falcón Hernández | Madrid, España
- ERP, CRM y Software
- WhatsApp: +34 662 47 06 45
- Telegram: falconsoft
- Email: mfalconsoft@gmail.com , falconsoft.3d@gmail.com
- Github: https://github.com/falconsoft3d
- linkedin: https://linkedin.com/in/marlon-falcón-3a2aa9a4

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
pip install -r /opt/odoo/server/requirements.txt
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
addons_path = /opt/odoo/server/addons,/opt/odoo/server/extra-addons/odoo_chile_community,/opt/odoo/server/extra-addons/odoo-modulos-3ros,/opt/odoo/server/extra-addons/odoo_general,/opt/odoo/server/extra-addons/odoo_chile_rrhh,/opt/odoo/server/extra-addons/odoo-modulos-web,/opt/odoo/server/extra-addons/odoo_general_web
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
nano /etc/postgresql/10/main/pg_hba.conf
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

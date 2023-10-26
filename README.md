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

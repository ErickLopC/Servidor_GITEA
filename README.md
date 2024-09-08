# Servidor_GITEA

## [REDES COMUNICACION](https://github.com/ErickLopC/COMUN_REDES)


# CONTENIDO
1. [Configuracion inicial](#Configuracion-inicial)
2. [Dependencias](#Dependencias)
3. [Base de datos](#Base-de-datos)
4. [Instalacion](#Instalacion)
5. [Funcionamiento](#Funcionamiento)
6. [References](#References)
7. [Solucion Problemas](#Sol-problem)
8. [Desinstalar GITEA](https://github.com/ErickLopC/Desins-Gitea)
9. [Mudar Base de datos](#Move-DB)
10. [FUTURES](#FUTURES)
11. [](#)
12. [](#)


Para la instlacion se requienen conocer comandos de ubuntu, debian o similares para montar  configurar sd y algunas otras configuraciones para ello visitar para algunos comandos de ubuntu  

https://github.com/ErickLopC/comandos-Ubuntu  

para cambiar el arranbque automtico de usb externa 

https://github.com/ErickLopC/cambio-fomat-usb

ademas de para tener una base de datos montada en una memoria externa visitar 


https://github.com/ErickLopC/baseDatosExterna



apara hacer la instalacion completa de Gitea en una memoria externa realizamos los siguientes pasos de esta documentacion **Configuracion inicial**
  despues la de **base de datosd en una memoria extena** para despues seguir con **Base de datos** con esta se acaba de configurar la base de datos externa finalmente para acabar de configurar gutea relizamos lo de **Instalacion**  una vez termoinado pasamos con **Funcionamiento** .

# Configuracion inicial

vER LAS IMAGENES QUE TENEMOS EN DOCKER
```
docker ps

```

debe aparecer 

**CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES**

Lo qu indicaria que ya se tiene instalado docker y seguimos con l ainstalacion

En caso de no tener instalado

[Instalar Docker CMD](https://github.com/ErickLopC/dockerNativoComandos)


# Dependencias 
```
sudo apt install curl
sudo apt -y install apt-transport-https
sudo apt-get install gnupg2
sudo apt-get install software-properties-common
sudo apt install vim -y
sudo apt install fail2ban
sudo apt-get install ntfs-3g
```

descargar las keys 
```
curl -fsSL https://download.docker.com/linux/debian/gpg | sudo apt-key add -
```

```
sudo apt-key fingerprint 0EBFCD88
```

echo "deb [arch=armhf] https://download.docker.com/linux/debian \

$(lsb_release -cs) stable " | \

```
sudo usermod -a -G docker ELC 
```



```


```


```
-
```
# cuando ya se tenga instaldo DOCKER realizamosd los siguientes pasos

```
docker ps

```

```
nano docker-compose.yml

```

Colocar lo siguiente 
```
services:
  gitea:
    image: gitea/gitea:latest
    container_name: gitea
    restart: always
    ports:
      - "3000:3000"
      - "222:22"
    volumes:
      - /home/ELC3NAS/gitea:/data
    environment:
      - USER_UID=1000
      - USER_GID=1000

```


```
docker-compose up -d
```



Por si hay detalles con la instalacion del docker compose se realiza lo siguine (se instala nuevamente

**Descarga la versión de docker-compose**
 
Puedes descargar la última versión de docker-compose usando el siguiente comando:
```
VERSION=$(curl --silent "https://api.github.com/repos/docker/compose/releases/latest" | grep -Po '"tag_name": "\K.*?(?=")')
sudo curl -L "https://github.com/docker/compose/releases/download/${VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

```
**Haz ejecutable el binario descargado**

Después de descargar docker-compose, necesitas darle permisos de ejecución:

```
sudo chmod +x /usr/local/bin/docker-compose

```

 **Verifica la instalación**
 
Para confirmar que docker-compose se ha instalado correctamente, verifica la versión:

```
docker-compose --version

```

y regreamos a ejecutar el; comando anterior para acbar de configurar, una vez ya configurado el composer

# Base de datos
CUENTA ROOT 
```
su -l

or

sudo su
```
Instalar base de datos
```
apt install mariadb-server nginx git

```
activar servicio de MariaDB 

**A PARTIR DE ESTA PARTE SE PUEDE SEGUIR CON LA CONFIGURACION DE LA BASE DE DATOS UNA VEZ YA SE TENGA CONFIGURADA LA BASE DE DATOS EXTERNA CON EL ALMACENAMIENTO EXTERNO**

https://github.com/ErickLopC/baseDatosExterna


ejecutar el servicio de bria db al ajecer el boot el servidor
```
systemctl enable mariadb

```

```
sudo mysql_secure_installation
```

configuracion 

Al pedir contraseña precionar enter 

Al pedir el modo socket precionar **N**

Precionar enter  -> oiNGRESAR NUEVA CONTRASE;A

enter 

enter

enter  ...
```
-
```
reconseña 

ERICKmendoza2000
```
sudo mysql -u root -p

```
Entramos al servidor mariaDB

Crramos la base de datos para gitea
```
CREATE DATABASE gitea;
```

Creamos cuenta de usuario con previlegios de gitea

```
GRANT ALL PRIVILEGES ON gitea.* TO 'gitea'@'localhost' IDENTIFIED BY 'ERICK_power_2000@';
```

Guardamos los cambios 

```
FLUSH PRIVILEGES;
```
Salimos con 

```
exit;

```
-
---

-
-

-

# Instalacion

```
sudo adduser --system --shell /bin/bash --gecos 'Git Version Control' --group --disabled-password --home /opt/git git
```

Verificar el direcciorio creado de git con duseñpo git y grupo git 
```
ls -la /opt/

```

Debe de aparecer que se agrego la siguiente linea 

**drwxr-xr-x  2 git  git  4096 Aug  8 07:30 git**

---

---

---

```
wget -O gitea https://dl.gitea.io/gitea/1.15.4/gitea-1.15.4-linux-arm-6

```

```
wget -O gitea  https://dl.gitea.com/gitea/1.22.0/gitea-1.22.0-linux-arm-6

```

---

---

---

```
mv git* /usr/local/bin/gitea

```


```
chmod +x /usr/local/bin/gitea

```



```
gitea --version

```


Creacion de los directorios para ponerla en marcha 
```
mkdir -p /etc/gitea /var/lib/gitea/{custom, data,indexers,public,log}

or

mkdir -p /etc/gitea /var/lib/gitea/custom /var/lib/gitea/data /var/lib/gitea/indexers /var/lib/gitea/public /var/lib/gitea/log


```


cambiamos los atributos al grupu git gruopo git 

```
chown git:git /var/lib/gitea/{data,indexers,log}
```
Cambiamos los permisos a lao sirectorios

```
chmod 750 /var/lib/gitea/{data,indexers,log}
```

```
chown root:git /etc/gitea
```

```
chmod 770 /etc/gitea

```

```
ls -la /var/lib/gitea/

```

nos aparecera algo como esto 

drwxr-xr-x  8 root root 4096 Jul 23 22:49 .

drwxr-xr-x 33 root root 4096 Jul 23 22:45 ..

drwxr-xr-x  2 root root 4096 Jul 23 22:45 {custom,

drwxr-xr-x  2 root root 4096 Jul 23 22:49 custom

drwxr-x---  2 git  git  4096 Jul 23 22:49 data

drwxr-x---  2 git  git  4096 Jul 23 22:49 indexers

drwxr-x---  2 git  git  4096 Jul 23 22:49 log

drwxr-xr-x  2 root root 4096 Jul 23 22:49 public

Crear ficheros para manejar gitea
```
nano /etc/systemd/system/gitea.service

```


```
[Unit]
Description=Gitea (Git with a cup of tea)
After=syslog.target
After=network.target
After=mysql.service

[Service]
LimitMEMLOCK=infinity
LimitNOFILE=65535
RestartSec=2s
Type=simple
User=git
Group=git
WorkingDirectory=/var/lib/gitea/
ExecStart=/usr/local/bin/gitea web -c /etc/gitea/app.ini
Restart=always
Environment=USER=git HOME=/opt/git GITEA_WORK_DIR=/var/lib/gitea

[Install]
WantedBy=multi-user.target
```


```
systemctl daemon-reload
```

```
systemctl enable gitea
```

```
systemctl start gitea
```

```
systemctl status gitea
```

Verificacion que el puerto este activo 

```
ss -antpl | grep 3000
```

Nos aparecera algo como 

LISTEN 0      4096               *:3000            *:*    users:(("gitea",pid=18043,fd=6)) 

Esta a la escuha de ese puerto 


Ahora configurar el servidor wed  poara que nos sirva por el puerto 80

```
nano /etc/nginx/conf.d/gitea.conf

```
colocar 
```
server{
  listen 80;
  server_name gitea.drivemeca.com;
  access_log /var/log/nginx/gitea_access.log;
  error_log /var/log/nginx/gitea_error.log;

 location / {
     proxy_pass http://localhost:3000;
 }
}
```
Verificamos que lo que se escribio correctamente

```
nginx -t
```
si todo esta configurado correctamente deberia aparecer 

nginx: the configuration file /etc/nginx/nginx.conf syntax is ok

nginx: configuration file /etc/nginx/nginx.conf test is successful

Habuliytar nginx cada vez que se reinicie 
```
systemctl enable nginx
```
```
systemctl restart nginx

```
```
systemctl status nginx

```
Editar
```
nano /etc/gitea/app.ini
```

Agregamos

```
DOMAIN         = gitea.drivemeca.com
ROOT_URL       = http://gitea.drivemeca.com/

```
Aguardamos cambios y salimos 

Reiniciamos gitea 

```
systemctl restart gitea

```

Verificamos que este corriendo GITEA 

```
systemctl status gitea

```

# Funcionamiento

cHECAR BIEN LA CONFIGURARAU=ION Y LOS PARTAMETROS QUE SE ENCUENTRA REMARCADOS EN NEGRITAS
```
http://IP-0-Dominio-gitea
```
PARA LA CONFIGURACION DE GITREA SE TIENE
```
Database Type **MySQL**

Host **127.0.0.1:3306**

Username   **gitea**

Password **Contraseña de la base D datos**

Database Name  **gitea**




Repository Root Path  **/var/lib/gitea/data/gitea-repositories**

Git LFS Root Path **/var/lib/gitea/data/lfs**

Run As Username  **git**

SSH Server Domain  **localhost**

SSH Server Port  **22**

Gitea HTTP Listen Port **3000**

Gitea Base URL **http://192.168.0.215:3000/**   <----------- CHANGE

Log Path  **/var/lib/gitea/log**


Optional Settings  **Administrator Account Settings**


EJEMPLO

Administrator Username **DIMAF_**

Password  **Elc2000@1230ABZ**

Confirm Password **ec667709@gmail.com**

```
--------------

----


---


# Sol problem

CaMmbios de ip de servidor
```
-
```
```
-
```




```
-
```



 # References

https://www.youtube.com/watch?v=ti76T4RNprg

https://www.youtube.com/watch?v=ZN3ykCT2T4Q

https://www.youtube.com/watch?v=bHtntM_KWn0


instlatr mediante portainer 

https://www.youtube.com/watch?v=oklkcFY8sHE

https://www.youtube.com/watch?v=oklkcFY8sHE

# Move DB

Solo se necesita mover la base en la meroria que se tiene a la que se desea


**Mover los Datos de MariaDB:**


Mueve los datos existentes de la ubicación predeterminada a la nueva ubicación en la memoria externa:
```
sudo mv /var/lib/mysql /mnt/external_drive/mariadb_data

```

```
-
```

```
-
```

# FUTURES

Instlar gitlab y hacer una tabla comparativa entre caracteristicas que odrece este y el tro, asi mo donde es mas recomentble instlar, base de datos y consas relativas.

```
-
```


```
-
```


```
-
```


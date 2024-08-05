# Servidor_GITEA

## [REDES COMUNICACION](https://github.com/ErickLopC/COMUN_REDES)


# CONTENIDO
1. [](#)
2. [](#)
3. [](#)
4. [](#)
5. [](#)
6. [](#)
7. [Solucion Problemas](#Sol problem)
8. [](#)
9. [](#)
10. [](#)


vER LAS IMAGENES QUE TENEMOS EN DOCKER
```
docker ps

```
dependencias 
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

```
-
```

```
-
```

# New instalation
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

ejecutar el servicio de bria db al ajecer el boot el servidor
```
systemctl enable mariadb

```

```
mysql_secure_installation
```

configuracion 

Al pedir contraseña precionar enter 

Al pedir el modo socket precionar **N**
```
-
```
reconseña 

ERICKmendoza2000
```
mysql -u root -p

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


```
adduser --system --shell /bin/bash --gecos 'Git Version Control' --group --disabled-password --home /opt/git git
```

Verificar el direcciorio creado de git con duseñpo git y grupo git 
```
ls -la /opt/
```


```
wget -O gitea https://dl.gitea.io/gitea/1.15.4/gitea-1.15.4-linux-arm-6

```


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

## AHORA IR IR AL NAVEGAOR 

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



references

https://www.youtube.com/watch?v=ti76T4RNprg

https://www.youtube.com/watch?v=ZN3ykCT2T4Q

https://www.youtube.com/watch?v=bHtntM_KWn0


instlatr mediante portainer 

https://www.youtube.com/watch?v=oklkcFY8sHE

https://www.youtube.com/watch?v=oklkcFY8sHE

# Servidor_GITEA

## [REDES COMUNICACION](https://github.com/ErickLopC/COMUN_REDES)

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
-
```
```
-
```









references


https://www.youtube.com/watch?v=ZN3ykCT2T4Q

https://www.youtube.com/watch?v=bHtntM_KWn0


instlatr mediante portainer 

https://www.youtube.com/watch?v=oklkcFY8sHE

https://www.youtube.com/watch?v=oklkcFY8sHE

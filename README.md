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

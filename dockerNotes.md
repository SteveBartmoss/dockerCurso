# Docker file

Define la forma en la que se construye un contenedor, implementa la version de node, copia archivos necesarios y los comandos que son necesarios al momento de constuir 
el contenedor

El siguiente es un ejemplo simple de un docker file 

```bash
FROM node:20-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

EXPOSE 8072

CMD ["npm", "run", "start:dev"]
```

# Docker compose yaml

Define que dependencias necesita un contenedor, como imagenes de bases de datos, volumenes si son necesarios, puertos que expone, configuracion de archivos .env

# Problemas de docker con synology

Aunque no lo parece, docker es completamente un sistema operativo diferente al que esta configurado en el servidor, por esta razon la configuracion de carpetas compartidas en red, puede que no este del todo claro.

## Docker no puede ver los archivos

Si no tenemos configurado el montaje de la unidad compatida en red, dentro de docker desktop ya que esta es la instancia que se puede ver desde los contenedores, en mi caso estaba usando una configuracion para desarrollo, donde simplemente usaba las credenciales de windows para poder ver la carpeta, bueno la sorpresa es que docker-desktop no puede ver estas carpetas

### Montar el volumen

Quiza esto no es muy recomendable pero es la forma en la que pude ver los volumentes compartidos por un synology compartido en red

```powershell
wsl -d docker-desktop
```

El comando anterior nos permite abrir una terminal del sistema operativo de docker-desktop y despues tenemos que intalar las utilidades necesarias para montar el volument

```bash
apk add cifs-utils
```

Ahora creamos el montaje de la carpeta, con el siguiente comando

```bash
mkdir -p /mnt/synology
```

con eso creamos el punto de montaje para la carpeta en red, ahora montamos el volumen red con el siguiente comando

```bash
mount -t cifs //192.168.1.5/Pruebas /mnt/synology -o username=Admin,password=admin,vers=3.0,uid=1000,gid=1000
```

En el comando debemos cambiar la direccion ip y la carpeta que queremos montar asi como el user name y el password que usamos en la carpeta compartida en red

```bash
ls /mnt/synology
```

con el comando anterior podemos verificar el contenido de la carpeta que montamos

### Usar el montaje en los contenedores de docker

Ahora que tenemos montamos el volumen, tenemos que usar esa ruta en los volumentes del docker compose

```yaml
volumes:
  - /mnt/synology:/data
```

### probar el acceso desde el contenedor

```yaml
docker exec -it caroline-back-dev sh
ls /data
```
Con esto deberiamos ver los archivos desde la carpeta compartida de red en el contenedo donde ejecutemos el comando, si podemos verlos entonces se pueden usar los recursos de 
la carperta compartida en red desde el bakend o en caso de que sea el front end tambien







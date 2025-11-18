

# Bases de docker

## Contenedores

### pull

Permite descargar una imagen en especifico para docker desde docker hub o si se especifica se usa un origen diferente

```bash
docker pull IMAGE_NAME #permite jalar una imagen
```

### container run

Permite ejecurar un contenedor, lo que tambien es una instancia de una imagen que tenemos descargado

```bash
docker container run hello-world
```

### ls

Permite lista los contenedores, si se usa sin el parametro '-a' se muestran solo los contenedores activos, se tiene que usar el parametro -a para poder listar todos los contenedores

```bash
docker container ls -a
```

### rm

Permite borrar un contenedor al pasar el id del contenedor que se quiere eliminar

```bash
docker container rm CONTAINER_ID
```

### detached 

Es una opcion que se pasa al comando run para indicar que queremos correr el contenedor sin que este mostrando logs en la consola y pode usar la consola para algo mas

```bash
docker container run -d IMAGE_NAME
```

### publish

Es una opcion que permite publicar un contenedor en el puerto especificado

```bash
docker container run -d -p 3000 IMAGE_NAME
```

### start

```bash
docker container start CONTAINER_ID
```

### stop

Permite detener un contenedor en especifico

```bash
docker container stop CONTAINER_ID
```

## Imagenes

### ls

Permite listar todas las imagenes que estan instaladas

```bash
docker image ls 
```

### rm

Permite borrar una imagen que tenemos instalada

```bash
docker image rm CONTAINER_ID
```

## Variables de entorno

Son parametros que se pueden pasar al momento de correr un contenedor, en este caso se esta pasando la variable POSTGRES_PASSWORD

```bash
docker run --name some-postgres -e POSTGRES_PASSWORD=prueba -d postgres
```
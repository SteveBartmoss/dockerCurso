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


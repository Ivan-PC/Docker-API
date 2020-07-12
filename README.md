# Docker-API
API escrita en Node JS que levanta un servidor en el puerto 3000 e intenta conectarse a una Base de datos MongoDB, se utilizara para mostrar como generar una imagen a partir de un archivo Dockerfile y luego ejecutar un contenedor a partir de esta.

La app espera un servicio ejecutandose localmente en el puerto 3000
http://localhost:3000/users-db

Nota: Se debe tener instalado Docker

# Actualizar dependencias
npm install

# Comando para generar la imagen segun el docker file existente
docker build -t api-node:ivan . 

# Crear un Volume de Datos Docker
docker volume create dbData 

# Ejecutar un Contenedor con MongoDB y montarle el volume
docker run -d --name db --mount src=dbData,dst=/data/db mongo 

# Estructura de Datos requerida
- Tabla users
- Campos name

## Comandos 

- Crear BD:
 use myDB 
- Crear tabla y registro: 
 db.users.insert({"name":"Maria"}) 
- Validar el insert: 
 db.users.find() 
- Salir de mongo:  
 Exit 

# Ejecutar Contenedor de la API
docker run -d  --env MONGO_URL=mongodb://db:27017/myDB -p 3000:3000 --name api api-node:ivan 

# Conectar contenedores a una Red, si no existe crearla
docker network ls
docker network create --attachable red-taller 
docker network connect red-taller db 
docker network connect red-taller api 

# Imagen publica de esta app
docker pull ivanpc/api-node:ivan

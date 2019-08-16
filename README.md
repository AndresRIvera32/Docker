# Docker
informacion docker

Comandos Docker principales:

# crear una imagen a partir de un archivo Dockerfile
Docker build -t nombre_imagen_contexto .

# si el archivo Dockerfile esta en otro path ponemos
Docker build -t nombre_imagen_contexto ./path

# correr un contenedor a partir de una imagen ya creada
* con -d especificamos que corra en segundo plano
* con -p indicamos los puertos por lo que en este ejemplo el 8001 hace referencia a nuestra maquina
* y el puerto 8080 es el puerto que expone mi contenedor
* --name especificamos el nombre de nuestro contenedor
* miImagen es la imagen que tomamos como referencia ya creada

Docker run -d -p 8001:8080 --name contenedor-demo miImagen

# nos permite mirar los logs de un contenedor docker
Docker logs contenedor-demo

# nos permite mirar todas las propiedades de un contenedor como su ip, puertos etc..
Docker inspect contenedor-demo

# nos permite entrar al contenedor conectandonos via ssh
docker exec -it contenedor-demo bash
docker exec -it contenedor-demo sh

# nos permite parar un contenedor
docker stop contenedor-demo

# nos permite inicializar un contenedor ya detenido
docker start contenedor-demo

# nos permite eliminar contenedores
Docker rm -f contenedor_demo

# nos permite eliminar imagenes
Docker rmi -f miImagen

# Ejemplo imagen de mysql

docker run -d -p 3310:3306 --name mysql_server \ -e MYSQL_ALLOW_EMPTY_PASSWORD=yes \ -e MYSQL_ROOT_PASSWORD=toor -e MYSQL_DATABASE=demobd \ -e MYSQL_ROOT_HOST=% \ mysql:latest --default-authentication-plugin=mysql_native_password

¡¡IMPORTANTE!!
--default-authentication-plugin=mysql_native_password 
* esta propiedad nos permite autenticarnos desde afuera de nuestro contenedor.

# Desplegar docker en AWS EC2

1. instalar docker en nuestra EC2/ sudo amazon-linux-extras install docker
2. subir nuestra imagen a nuestro repo en docker hub / docker push nombreUsuario_docker_hub/imagen_local
3. para correr la imagen en nuestro contenedor desde una imagen en docker hub tenemos que teclear el comando:
sudo usermod -aG docker $USER
4. corremos nuestro contenedor a partir de la imagen que tengamos en nuestro docker hub:
docker run -p 8050:8080 nombreUsuario_docker_hub/imagen_local 



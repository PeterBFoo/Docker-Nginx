# Docker Nginx

### Dockerización de una imagen nginx

En Docker Hub se alojan todo tipo de imágenes, por lo tanto, se accede al portal y se busca la imágen oficial de nginx.
<img width="1680" alt="Captura de pantalla 2022-03-15 a las 14 41 40" src="https://user-images.githubusercontent.com/91556382/158396677-97f635ee-b2f1-4b0c-851a-c310db0d5910.png">

Seguidamente, según pone en la página realizar:

```bash
docker pull nginx

```

<img width="568" alt="Captura de pantalla 2022-03-15 a las 14 42 36" src="https://user-images.githubusercontent.com/91556382/158397001-ab4aaf26-77da-45dc-b518-15ab09a07cd6.png">

De esta manera, se dispondrá de la imágen nginx para poder crear contenedores a partir de ella. Para crear un contenedor, nginx al ser un servidor web, se tendrá que indicar en qué puerto se decide escuchar. Por lo tanto...

<img width="639" alt="Captura de pantalla 2022-03-15 a las 14 43 07" src="https://user-images.githubusercontent.com/91556382/158397168-f4e13b07-7ade-433e-a4f3-1929dc83f50c.png">

Ahora, si se accede al navegador y se accede a http://localhost:8080 con el contenedor activo, aparecerá un mensaje de bienvenida de nginx:

<img width="824" alt="Captura de pantalla 2022-03-15 a las 14 43 30" src="https://user-images.githubusercontent.com/91556382/158397694-ff9fbd11-98fd-4588-a489-bf6af6e7da55.png">

Para detener el contenedor:

```bash
docker stop web
```

Si se quiere modificar el contenido de la web, se deberá crear un Dockerfile para sustituir el mensaje de bienvenida de nginx por uno propio, además de un index.html propio. Por lo tanto, dentro de un directorio a elección, crear los directorios /nginx/site-content y dentro de site-content estará el archivo html, en cambio, el docker file estará en nginx/.
El Dockerfile contiene los siguientes parámetros.

<img width="660" alt="Captura de pantalla 2022-03-15 a las 14 53 52" src="https://user-images.githubusercontent.com/91556382/158398050-9825fea0-595b-4655-925f-657222b002d2.png">

Y el index.html estos otros:

<img width="295" alt="Captura de pantalla 2022-03-15 a las 15 23 53" src="https://user-images.githubusercontent.com/91556382/158399265-6bc1df89-4169-4e31-98ef-56e88efb796a.png">

Ahora, posicionándose en el directorio nginx/ realizar:

```bash
docker build -t webserver .
```
<img width="679" alt="Captura de pantalla 2022-03-15 a las 15 02 41" src="https://user-images.githubusercontent.com/91556382/158399523-98baa996-1a62-44d5-b2e0-b560d97c1dc1.png">

Ahora que la imágen ha sido creada, resta crear el contenedor a partir de ella:

```bash
docker run --rm -d -p 8080:80 --name web webserver
```

<img width="597" alt="Captura de pantalla 2022-03-15 a las 15 03 25" src="https://user-images.githubusercontent.com/91556382/158399693-799ff770-0290-479a-a2c1-239b4ae01d09.png">

Una vez creado el contenedor, al estar en modo "detached" estará activo hasta que se decida detenerlo. Por lo tanto, hay que volver a navegar a http://localhost:8080 para comprobar si está funcionando el cambio que hemos realizado.

<img width="1064" alt="Captura de pantalla 2022-03-15 a las 14 51 21" src="https://user-images.githubusercontent.com/91556382/158400071-0221919f-60a6-42ca-92c5-e21648894e6a.png">

---

### Usar la imágen creada en una VM de Microsoft Azure

Es posible subir la imágen recién creada a Docker Hub para después ser consumida por la VM de Microsoft Azure, simplemente se tendrá que instalar Docker en esa máquina para que pueda descargar la imágen y crear un contenedor sobre ella.


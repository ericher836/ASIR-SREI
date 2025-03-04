# Práctica Docker

## Primer Artículo
1. Ejecuta la imagen `hello-world`.

Para ejecutar la imagen hello-world, usamos el siguiente comando.

```
sudo docker run hello-world
```

![](/Tema3/img/Screenshot_15.png)

```
sudo docker ps -a
```

![](/Tema3/img/Screenshot_17.png)

```
sudo docker logs nombre_contenedor
```

![](/Tema3/img/Screenshot_28.png)

2. Muestra las imágenes Docker instaladas.

```
sudo docker images
```

![](/Tema3/img/Screenshot_19.png)

3. Muestra los contenedores Docker.

```
sudo docker ps -a
```

![](/Tema3/img/Screenshot_17.png)

## Segundo Artículo

1. Edita el fichero `Dockerfile`.

```
sudo git clone https://github.com/docker/getting-started-app.git
```

![](/Tema3/img/Screenshot_46.png)
![](/Tema3/img/Screenshot_47.png)

```
# syntax=docker/dockerfile:1

FROM node:lts-alpine
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
EXPOSE 3000
```

![](/Tema3/img/Screenshot_48.png)

2. Construye el contenedor.

```
sudo docker build -t getting-started .
```

![](/Tema3/img/Screenshot_49.png)

3. Ejecútalo.

```
sudo docker run -d -p 127.0.0.1:3000:3000 getting-started
```

![](/Tema3/img/Screenshot_50.png)
![](/Tema3/img/Screenshot_51.png)
![](/Tema3/img/Screenshot_52.png)

4. Crea una cuenta en [hub.docker.com](https://hub.docker.com).

![](/Tema3/img/Screenshot_53.png)
![](/Tema3/img/Screenshot_54.png)
![](/Tema3/img/Screenshot_55.png)
![](/Tema3/img/Screenshot_56.png)
![](/Tema3/img/Screenshot_57.png)

5. Publícalo.

```
sudo docker login -u nombre_usuario
```

![](/Tema3/img/Screenshot_58.png)

```
sudo docker tag getting-started nombre_usuario/getting-started:latest
```

![](/Tema3/img/Screenshot_59.png)

```
sudo docker commit nombre_contenedor nombe_repositorio
```

![](/Tema3/img/Screenshot_60.png)

```
sudo docker push nombre_repositorio
```

![](/Tema3/img/Screenshot_61.png)
![](/Tema3/img/Screenshot_62.png)



![](/Tema3/img4/Screenshot_1.png)

```yaml
version: '3.1'
services:
  frontend:
    container_name: temperaturas-frontend
    image: iesgn/temperaturas_frontend
    restart: always
    ports:
      - 8081:3000
    environment:
      TEMP_SERVER: temperaturas-backend:5000
    depends_on:
      - backend
  backend:
    container_name: temperaturas-backend
    image: iesgn/temperaturas_backend
    restart: always
```

```
sudo docker compose up -d
```

![](/Tema3/img4/Screenshot_3.png)

```
sudo docker ps
```

![](/Tema3/img4/Screenshot_4.png)

```
sudo docker network create red_temperaturas
```

![](/Tema3/img4/Screenshot_5.png)

```
sudo docker network create red_temperaturas
```

![](/Tema3/img4/Screenshot_6.png)

```
sudo docker network create red_temperaturas
```

![](/Tema3/img4/Screenshot_7.png)

```
sudo docker network create red_temperaturas
```

![](/Tema3/img4/Screenshot_8.png)

```
sudo docker network create red_temperaturas
```

![](/Tema3/img4/Screenshot_9.png)

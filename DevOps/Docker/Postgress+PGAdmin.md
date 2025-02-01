# Postgress + PgAdmin4

File: `docker-compose.yml`

```yml
services:
  db:
    container_name: postgres_container
    image: postgres
    environment:
      POSTGRES_USER: root
      POSTGRES_PASSWORD: root
      POSTGRES_DB: test_db
    ports:
      - "5432:5432"
  pgadmin:
    container_name: pgadmin4_container
    image: dpage/pgadmin4
    restart: always
    environment:
      PGADMIN_DEFAULT_EMAIL: manujgogoi@gmail.com
      PGADMIN_DEFAULT_PASSWORD: Kakotibari#123
    ports:
      - "5050:80"
```

Then execute the following commands

```sh
docker-compose up
```

In another terminal

```sh
docker container ls
```

Copy the Id of the postgres container and then run the following command to get the Ip address of the container

```sh
docker inspect 126d85a1238e
```

It is `"IPAddress": "172.18.0.2"`

## Step two

- Go to `localhost:5050` in web browser
- Enter pgadmin email and password fields to login
- **Add New Server**
- In **General** enter db name
- In **Connection** enter postgress container Ip address: `172.18.0.2`
- Enter Username and password
- And Save

### Run Docker in detached mode

```sh
docker-compose up -d
docker-compose down
```

Other commands

```sh
docker volume ls
```

To delete volumes too

```sh
docker-compose down -v
```

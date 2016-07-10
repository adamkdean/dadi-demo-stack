## MongoDB

I use docker for this. I'm using Docker for Mac so that containers publish to localhost.

Create a volume:
```shell
docker volume create --name=mongodb-data
```

Run mongo 3.2:
```shell
docker run \
  --detach \
  --name mongodb-server \
  --volume mongodb-data:/data/db \
  --publish 27017:27017 \
  mongo:3.2 \
    --noprealloc \
    --smallfiles
```

(Optional) run mongo express and link to mongo:
```shell
docker run \
  --detach \
  --name mongo-express \
  --link mongodb-server:mongo \
  --publish 8081:8081 \
  mongo-express:0.30
```

## API

```shell
cd api
npm install
node node_modules/@dadi/api/utils/create-client.js
node main.js
```

## Web

```shell
cd web
npm install
node main.js
```

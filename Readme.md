# build 

## build the backend

```bash
git clone https://github.com/yawik-gdr/backend
cd backend
# create .env file
npm run build
npm run docker:build
```

## build the jobboard

```bash
git clone https://github.com/yawik-gdr/jobboard
cd jobboard
# create .env file
npm install
npm run build
npm run docker:build
```

## build the jobwizard

```bash
git clone https://github.com/yawik-gdr/jobwizard
cd jobwizard
# create .env file
npm install
npm run build
npm run docker:build
```

# deploy

## Start solr


```bash
git clone https://github.com/yawik-gdr/solrConfigAndDeployment
cd solrConfigAndDeployment
docker run -d -p 8983:8983 --name solrserver -v  `pwd`/contrib/conf:/my_core_config/conf solr:8 solr-precreate my_core /my_core_config
```

## start the backend

```bash
docker load --input /home/zprojet/jobbackend.tar 

docker run -p 3002:3000 \
-v  /home/zprojet/strapidata/data.db:/strapi/.tmp/data.db --link solrserver:solrserver \
-p 3004:1337 -d barais/jobbackend
```

## start the frontend

```bash

docker image rm barais/jobboard  barais/jobwizard 

docker pull barais/jobboard 
docker pull barais/jobwizard 

docker run -p 8084:80 -d barais/jobboard
docker run -p 8082:80 -d barais/jobwizard
```

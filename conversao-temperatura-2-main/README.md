# conversao-temperatura-2
Iniciativa Devops - Fabricio Veronez - Kube Dev

* Rodar Gerenciador de Pacotes: NPM 

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ npm install
```
* Rodar aplicação local

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ node server.js
Servidor rodando na porta 8080

```

* Construindo Dockerfile e Image

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker build -t orbite82/conversao-temperatura-2:v1 .
```

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker image ls
REPOSITORY                         TAG       IMAGE ID       CREATED             SIZE
orbite82/conversao-temperatura-2   v1        cb38c1e89678   40 seconds ago      1.05GB
```

* Reutilizando o cache: Alterando no arquivo server.js com comentário

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker build -t orbite82/conversao-temperatura-2:v1 .
Sending build context to Docker daemon  21.08MB
Step 1/7 : FROM node
 ---> e3cb0fb99b7c
Step 2/7 : WORKDIR /app
 ---> Using cache
 ---> 29cfbac4033d
Step 3/7 : COPY package*.json ./
 ---> Using cache
 ---> cfebe90cd5a6
Step 4/7 : RUN npm install
 ---> Using cache
 ---> 91347e7e514e
Step 5/7 : COPY . .
 ---> 334f8efdf92c
Step 6/7 : EXPOSE 8080
 ---> Running in d5deb26d374b
Removing intermediate container d5deb26d374b
 ---> 9c7379686556
Step 7/7 : CMD ["node", "server.js"]
 ---> Running in ae7aba5e1178
Removing intermediate container ae7aba5e1178
 ---> 1aa42081a58e
Successfully built 1aa42081a58e
Successfully tagged orbite82/conversao-temperatura-2:v1
```

* Testar a aplicação e imagem do Docker

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker container run -d -p 8080:8080 orbite82/conversao-temperatura-2:v1
cdc1a722b1c7cd00147bd077a83e983f1fa587105e1e328cff4935f7417c2e42
```

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker image ls
REPOSITORY                         TAG       IMAGE ID       CREATED             SIZE
orbite82/conversao-temperatura-2   v1        1aa42081a58e   4 minutes ago       1.05GB
```

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker container ls
CONTAINER ID   IMAGE                                 COMMAND                  CREATED              STATUS              PORTS                                             NAMES
1e6cde14b97b   orbite82/conversao-temperatura-2:v1   "docker-entrypoint.s…"   About a minute ago   Up About a minute   8080/tcp, 0.0.0.0:8080->80/tcp, :::8080->80/tcp   quirky_chatterjee
e7a1653c14f2   postgres                              "docker-entrypoint.s…"   3 hours ago          Up 3 hours          0.0.0.0:5432->5432/tcp, :::5432->5432/tcp         romantic_liskov
```

* Versão do Node

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ node --version
v14.19.3
```

* Atualizando Versão do Node: 16.X

Node.js v12.x:

```
$ curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -
$ sudo apt-get install -y nodejs

```
sudo apt-get install -f
sudo apt-get remove npm nodejs
sudo apt-get install npm nodejs

Dependências desencontradas e pacotes quebrados que impediam de instalar um programa conseguir resolver consegui resolver dando um:

sudo aptitude safe-upgrade
sudo aptitude update
sudo aptitude install npm
node -v

[Link](https://pt.stackoverflow.com/questions/215927/erro-npm-e-node-ubuntu)

* Versão Atualizada:16.X

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ node --version
v16.15.1
```

* Image nova V2

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker build -t orbite82/conversao-temperatura-2:v2 .
Sending build context to Docker daemon  21.08MB
Step 1/7 : FROM node:16.15.1
 ---> b59df4e04d61
Step 2/7 : WORKDIR /app
 ---> Using cache
 ---> 8bd5988d50c8
Step 3/7 : COPY package*.json ./
 ---> Using cache
 ---> 413594f09f93
Step 4/7 : RUN npm install
 ---> Using cache
 ---> adf5fb46a222
Step 5/7 : COPY . .
 ---> e1e918a9dc24
Step 6/7 : EXPOSE 8080
 ---> Running in e95bf87bd6ad
Removing intermediate container e95bf87bd6ad
 ---> 233e25db35ef
Step 7/7 : CMD ["node", "server.js"]
 ---> Running in cdb4423797f5
Removing intermediate container cdb4423797f5
 ---> b98110872971
Successfully built b98110872971
Successfully tagged orbite82/conversao-temperatura-2:v2

```

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker image ls
REPOSITORY                         TAG       IMAGE ID       CREATED          SIZE
orbite82/conversao-temperatura-2   v2        b98110872971   2 minutes ago    959MB
orbite82/conversao-temperatura-2   v1        1aa42081a58e   32 minutes ago   1.05GB
node                               16.15.1   b59df4e04d61   2 hours ago      907MB
node                               latest    e3cb0fb99b7c   2 hours ago      996MB
postgres                           latest    5b21e2e86aab   9 days ago       376MB

```

* Executando V2 container

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker container run -d -p 8080:8080 orbite82/conversao-temperatura-2:v2
a44744f98ef30ccd72911a615db92234c07a35045cb3d08abe44bf6200a7207c
```

* Docker push V1 e V2

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker push orbite82/conversao-temperatura-2:v1
The push refers to repository [docker.io/orbite82/conversao-temperatura-2]
8aa3297902eb: Pushed 
b2611ae55332: Pushed 
8d06b4cfacb9: Pushed 
676491776d22: Pushed 
8f2b79d5328d: Mounted from library/node 
693214157724: Mounted from library/node 
f2f715b72340: Mounted from library/node 
9e8a8e4e0b92: Mounted from library/node 
2fbabeba902e: Mounted from library/node 
ee509ed6e976: Mounted from library/node 
9177197c67d0: Mounted from library/node 
7dbadf2b9bd8: Mounted from library/node 
e7597c345c2e: Mounted from library/node 
v1: digest: sha256:28c8e4e7faf95e2d2a12040bd143fdead5f4464499d10c919c0455c9ca3ec48a size: 3054
```

```
┌─[orbite]@[orbite-desktop]:~/Iniciativa-Devops/conversao-temperatura-2/src
└──> $ docker push orbite82/conversao-temperatura-2:v2
The push refers to repository [docker.io/orbite82/conversao-temperatura-2]
5042a691a071: Pushed 
1d1568dd87f3: Pushed 
3d8a6c44f4c4: Pushed 
7afb0e318720: Pushed 
0830919801f6: Mounted from library/node 
802846f6da73: Mounted from library/node 
1a626c9c8e68: Mounted from library/node 
216157dba6a2: Mounted from library/node 
5d1a42aa54a1: Mounted from library/node 
80d46995af06: Mounted from library/node 
597ea5af36e6: Mounted from library/node 
8f534d0617ce: Mounted from library/node 
f14da82c36e2: Mounted from library/node 
v2: digest: sha256:fb0d520aaab79d4d1c5f602075581419ea0776f0e79849ada1f8d120a359423f size: 3053
```

* Docker Hub

[docker hub](https://hub.docker.com/repository/docker/orbite82/conversao-temperatura-2)

* Github Orbite

[My Github](https://github.com/orbite82/conversao-temperatura-2)
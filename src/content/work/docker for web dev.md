---
title: Docker for Web dev
publishDate: 2023-02-02 00:00:00
img: /assets/docker.webp
img_alt: plantes
description: |
  Durant ma formation, j'ai reuni tous les outils dev web de l'année dans une seule et image Docker, à déployer pour commencer un projet en quelques secondes.
tags:
  - Docker
  - Fast 
  - New Project
  
---

This image is a Linux with softwares for dev students

Default "docker pull nicolascir/nicodevdocker" DOES NOT WORK without TAG (version name), please read docker run examples below

2021-12-18 "v12" //ADDED angular example, UPDATED NPM 8.3.0

2021-12-10 "v11" //ADDED Strapi example , Laravel example

2021-12-09 "v10" //ADDED react example

2021-12-08 "v9" //ADDED vue example ADDED @vue/cli@4.5.15 , @vue/cli-service-global@4.5.15

2021-12-07 "v8" //UPDATED symfony example, ADDED codeigniter 4 example, ADDED unzip (6.0-25ubuntu1) , zip (3.0-11build1), php intl(2:7.4+75)

2021-11-23 "v7" //ADDED example folder, ADDED wget 1.20.3-1 / git 1:2.25.1-1

2021-11-11 "v6" //ADDED "project" folder for persistent linux/wsl folder

2021-11-10 "v5" //ADDED nano 4.8/curl 7.68.0-1ubuntu2.7/ Composer version 2.1.12 //UPDATED npm 8.1.3/ node v14.18.1/ Yarn1.22.15

2021-11-09 "v4" //ADDED Apache2-2.4.41/ Npm 6.14/Node 10.19/ Yarn 0.32/Mariadb 10.3.31/ Phpmyadmin 4.9.5/ mongodb 3.6.8

2021-11-08 "V1 V2 V3" // started from UBUNUTU 20.04.3 LTS official docker image

FIRST RUN

docker run -it -p 80:80 --name mydevcontainer nicolascir/nicodevdocker:v12

WHEN CONTAINER IS CLOSED, OPEN IT AGAIN USING :

docker start mydevcontainer

docker exec -it mydevcontainer bash

YOU CAN ADD NEEDED PORTS (example)

docker run -it -p 3000:3000 -p 80:80 -p 3306:3306 -p 1337:1337 -p 27017:27017 --name mydevcontainer nicolascir/nicodevdocker:v12

SHARED FOLDER FROM INSIDE DOCKER TO YOUR LINUX / WINDOWS -> CREATE A "-v" VOLUME (linux: where your wrote the command line, windows: in explorer type \ \ wsl$ )

docker run -it -p 3000:3000 -p 80:80 -v ${PWD}/project:/project --name mydevcontainer nicolascir/nicodevdocker:v12

NOT RECOMMENDED AT ALL, TO EDIT FILES YOU CAN USE Visual Studio Code "remote explorer" ADDON (microsoft 6M downloads)

CONTENT :

UBUNUTU 20.04.3 LTS / NODE : 14.18.1 / NPM : 8.3.0 / YARN : 1.22.15 / NANO : 4.8 / CURL : 7.68.0-1ubuntu2.7 / COMPOSER : 2.1.12 / wget 1.20.3-1 / git 1:2.25.1-1 /unzip(6.0-25ubuntu1) / zip (3.0-11build1) / php intl(2:7.4+75) / @vue/cli@4.5.15 / @vue/cli-service-global@4.5.15

APACHE2 2.4.41 , port 80 , PHP : 7.4.3 , START MANUALLY : sudo service apache2 start

MARIADB : 10.3.31 , port 3306 , START MANUALLY sudo service mysql start , root // no password , admin//adminadmin and coincoin//coincoin are users with all access granted

PHPMYADMIN : 4.9.5deb2 , WORKS IF APACHE2 AND MYSQL STARTED : http://127.0.0.1/phpmyadmin , login : admin//adminadmin

MONGODB : 3.6.8 , port 27017 , START MANUALLY : sudo service mongodb start

HOW TO USE PRE-INSTALLED SYMFONY PROJECT

docker run -it -p 8000:8000 -p 80:80 --name symfonyexample nicolascir/nicodevdocker:v12

service apache2 start && service mysql start

cd examples/symfonyexample

symfony serve -d

HOW TO CREATE NEW SYMFONY PROJECT

docker run -it -p 8000:8000 -p 80:80 --name symfonycontainer nicolascir/nicodevdocker:v12

service apache2 start && service mysql start

cd project

composer create-project symfony/website-skeleton my_project_name

cd my_project_name

symfony serve -d

modify .env and add

DATABASE_URL="mysql://admin:adminadmin@127.0.0.1:3306/my_project_name?serverVersion=mariadb-10.3.31"

HOW TO USE PRE-INSTALLED Codeigniter4

docker run -it -p 80:80 --name ci4examplecontainer nicolascir/nicodevdocker:v12

mv /examples/codeigniter4example/ /var/www/html/

service apache2 start && service mysql start

visit http://localhost/codeigniter4example/public

HOW TO CREATE NEW Codeigniter4

docker run -it -p 80:80 --name ci4container nicolascir/nicodevdocker:v12

cd var/www/html

composer create-project codeigniter4/appstarter ci4project

chmod -R 777 ci4project

cd ci4project

rename env to .env

edit inside .env : CI_ENVIRONMENT = development

edit inside .env database parameters localhost admin//adminadmin

service apache2 start && service mysql start

visit http://localhost/ci4project/public

HOW TO USE PRE-INSTALLED VUE JS

docker run -it -p 8080:8080 -p 80:80 --name vueexamplecontainer nicolascir/nicodevdocker:v12

cd project

cd vueexample

yarn serve

visit localhost:8080

HOW TO CREATE NEW VUE JS

docker run -it -p 8080:8080 -p 80:80 --name vuecontainer nicolascir/nicodevdocker:v12

cd project

vue create myvue

cd myvue

yarn serve

visit localhost:8080

HOW TO USE PRE-INSTALLED REACT

docker run -it -p 3000:3000 -p 80:80 --name reactexamplecontainer nicolascir/nicodevdocker:v12

cd examples/reactexample

yarn start

visit localhost:3000

HOW TO CREATE NEW REACT

docker run -it -p 3000:3000 -p 80:80 --name reactcontainer nicolascir/nicodevdocker:v12

cd project

npx create-react-app reactproject

cd reactproject

yarn start

visit localhost:3000

HOW TO USE PRE-INSTALLED ANGULAR

docker run -it -p 4200:4200 -p 80:80 --name angularexamplecontainer nicolascir/nicodevdocker:v12

cd examples/angularexample

ng serve --host 0.0.0.0

visit localhost:4200

HOW TO CREATE NEW ANGULAR

docker run -it -p 4200:4200 -p 80:80 --name angularcontainer nicolascir/nicodevdocker:v12

cd project

ng new angularproject

cd angularproject

ng serve --host 0.0.0.0

visit localhost:4200

HOW TO USE PRE-INSTALLED STRAPI

docker run -it -p 1337:1337 -p 80:80 --name strapiexamplecontainer nicolascir/nicodevdocker:v12

cd examples/strapiexample

yarn develop

visit http://localhost:1337/admin

HOW TO CREATE NEW STRAPI

docker run -it -p 1337:1337 -p 80:80 --name strapicontainer nicolascir/nicodevdocker:v12

cd project

npx create-strapi-app my-project --quickstart

visit http://localhost:1337/admin

HOW TO USE PRE-INSTALLED LARAVEL

docker run -it -p 80:80 --name laravelcontainer nicolascir/nicodevdocker:v12

cd examples

mv laravelexample/ /var/www/html/

service apache2 start && service mysql start

visit localhost/laravelexample/public

HOW TO CREATE NEW LARAVEL

docker run -it -p 80:80 --name laravelcontainer nicolascir/nicodevdocker:v12

cd /var/www/html

composer create-project laravel/laravel laravelproject

chmod 777 -R laravelproject

cd laravelproject

service apache2 start && service mysql start

visit localhost/laravelproject/public

WORDPRESS NOT COMPATIBLE ! instead use this very good docker compose https://gist.github.com/bradtraversy/faa8de544c62eef3f31de406982f1d42

note : to upload your own container on docker.io , you need a free account (windows : you need to be logged in docker GUI) , in docker website create a repository.

run existing image, which become a container, add anything inside this container, then

docker commit containername imagename

docker tag imagename yourusername/reponame:versionname

docker push yourusername/reponame:versionname

//example I used

docker commit nicotrainv4 nicodevdockerv5

docker tag nicodevdockerv5 nicolascir/nicodevdocker:v5

docker push nicolascir/nicodevdocker:v5
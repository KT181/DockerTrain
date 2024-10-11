# DockerTrain
DockerTrain on debian

---------------------------------------------------------------------------------------2024/10/11



docker pull httpd    ---拉映像檔

指令:  Host:container

image-------->container

              容器(記憶體)
              
docker volume create httpd-volume

docker run -itd --name http-container -p "8080:80" -v http-volume:/opt httpd

生成會有亂碼

docker ps -----------docker進程

注意提示符號 本機 or  docker

docker exec -it http-container /bin/bash

root@sda5d56sa4d5s6a1d56  -----顯示

exit 跳出

docker volume inspect httpd-volume

找到volume資訊

sudo ls -l /opt/docker/volumes/httpd-volume/_data


以上建立container


docker stop http-container http-container

docker ps

docker network create http-network

docker run -itdd --name http-client -p "8080:80" --network http-network httpd

docker rm http-server

docker run -itdd --name http-server -p "8081:80" --network http-network httpd

docker exec -it http-client /bin/bash

如果沒有ping

先apt-get update

在apt-get -y iputils-ping


跳出後docker network list就可以抓到網路了

bridge

host

null   ---三型態



docker run -itd --name http-host --network http-network httpd


建立MySQL服務

mkdir MySQL

cd MySQL

sudo apt-get update

sudo apt-get install -y vim

vim Dockerfile

FROM mysql:8.0.39-debian

RUN mkdir /app

WORKDIR /app

ENV MYSQL_ROOT_PASSWORD=password*

ENV MYSQL_DATABASE=knu

ENV MYSQL_USER=user

ENV MYSQL_PASSWORD=password*


EXPOSE 3306

CMD ["mysqld"]





docker build -t mysql-image .



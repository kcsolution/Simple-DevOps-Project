
1. how to search a docker image in hub.docker.com
```sh
docker search httpd
```
2. Download a docker image from hub.docker.com
```sh
docker image pull <image_name>:<image_version/tag>
```

3. List out docker images from your local system
```sh
docker image ls
```

4. Create/run/start a docker container from image
```sh
docker run -d --name <container_Name> <image_name>:<image_version/tag>

d - run your container in back ground (detached)
```

5. Expose your application to host server
```sh
docker run -d  -p <host_port>:<container_port> --name <container_Name> <image_name>:<Image_version/tag>

docker run -d --name httpd_server -p 8080:80 httpd:2.2
```

6. List out running containers
```sh
docker ps
```

7. List out all docker container (running, stpooed, terminated, etc...)
```sh
docker ps -a
```

8. run a OS based container which interactive mode (nothing but login to container after it is up and running)

```sh
docker run -i -t --name centos_server centos:latest
i - interactive
t - Terminal
```

9. Stop a container 
```sh
docker stop <container_id>
```

10. Start a container which is in stopped or exit state

```sh
docker start <container_id>
```
11. Remove a container e imagens

```sh
docker rm <container_id>

Remove container:

 docker stop $(docker ps -a -q)
 docker rm $(docker ps -a -q)

Remove all images
 docker rmi $(docker images)
 
--Removing Volumes
Remove one or more specific volumes - Docker 1.9 and later
Use the docker volume ls command to locate the volume name or names you wish to delete. Then you can remove one or more volumes with the docker volume rm command:

List:

 docker volume ls
Remove:

  docker volume rm volume_name volume_name
```

12. login to a docker container
```sh
docker exec -it <container_Name> /bin/bash
```
13. Alterar o hone do Tomcat no container
 
```
 [root@docker-server ~]# docker exec -it tomcat-container /bin/bash
  root@004482c1f7b1:/usr/local/tomcat# ls
  BUILDING.txt  CONTRIBUTING.md  LICENSE  NOTICE  README.md  RELEASE-NOTES  RUNNING.txt  bin  conf  include  lib  logs  native-jni-lib     temp  webapps  webapps.dist  work
  root@004482c1f7b1:/usr/local/tomcat# cd webapps
  root@004482c1f7b1:/usr/local/tomcat/webapps# cd ..
  root@004482c1f7b1:/usr/local/tomcat# cd webapps.dist/
  root@004482c1f7b1:/usr/local/tomcat/webapps.dist# ls
  ROOT  docs  examples  host-manager  manager
  root@004482c1f7b1:/usr/local/tomcat/webapps.dist# cp -R * ../webapps
  root@004482c1f7b1:/usr/local/tomcat/webapps.dist# ls
  ROOT  docs  examples  host-manager  manager
  root@004482c1f7b1:/usr/local/tomcat/webapps.dist#

14. Copiar arquivo de dentro do Container (cópia de arquivos para restabelecer pagina principal do Tomcat)
```
  [dockeradmin@docker-server ~]$ cat Dockerfile
  FROM tomcat:latest

  MAINTAINER AR Kleber

  COPY ./webapp.war /usr/local/tomcat/webapps

  ADD .  /usr/local/tomcat/webapps.dist
  WORKDIR  /usr/local/tomcat/webapps.dist
  RUN cp -R *  ../webapps

# Docker-command-For-install-redis-image-Docker Image ls
Docker Run --Name of our imaeg 
 <Find our image in hub.docker >
docker pull redis

docker ps -a ===> show me all container that ...
docker run -it nameOfOurImage  
====================================================
command  for install redis on docker windows 
 docker pull redis 
docker rin -d -p 6379:6379 --name redis redis 
docker loges redis 
docker exec -it sh 
docker-cli
show the redis on docke rtest for that 
pong 
==========
 
 
 
 
 
 =================================
 Create new container  
   a) docker run -i -t ubuntu /bin/bash
   b) docker run --name rails_dev_container -i -t ubuntu ubuntu /bin/bash
   The command line flags - i -t provide an interactive shell in the new container

2. Show running docker containers    ==> docker ps

3. Show list of current containers   ==> 
   a) docker ps -a   (Show all containers, both stopped and running)
   b) docker ps -n x (shows the last x containers, running or stopped, ex: docker ps -n 5)

4. Show last container that was run (whether is is running or stopped)  ==> docker ps -l

5. List docker images               ==> docker images

6. Delete a container               
   a) docker rm <container_id>    (ex: docker rm aa3f365f0f4e)
   b) docker rm <container_name>  (ex: docker rm rails_dev_container)
   
7. Delete all containers            ==> docker rm $(docker ps -a -q)

8. Delete an image                  ==> docker rmi <image_id>

9. Delete all images                ==> docker rmi $(docker images -q)

Start a stopped container
  a) docker start <container_id>    (ex: docker start aa3f365f0f4e)
  b) docker start <container_name>  (ex: docker start rails_dev_container)
  
Attach to a container
  a) docker attach <container_id>   (ex: docker attach aa3f365f0f4e)
  b) docker attach <container_name> (ex: docker attach rails_dev_container)

Creating daemonized containers
  docker run --name daemon_container -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"
  (-d flag detachs the container to the background)
  
To see what's happening inside the container
  docker logs rails_dev_container
  docker logs -f rails_dev_container  (like the tail -f)
  docker logs -ft rails_dev_container (prefix log entries with timestamps)
  docker logs --tail 10 daemon_container  (get the last 10 lines of the log)
  docker logs --tail 0 -f daemon_container (follow the logs without having to read the whole log file)
 
Inspecting the container's processes
  docker top daemon_container

Running a process inside a container
  a) Background 
     docker exec -d daemon_container touch /etc/new_config_file
  b) Interactive
     docker exec -t -i daemon_container /bin/bash

Stopping a daemonized container
  docker stop daemon_container
  or
  docker stop aa3f365f0f4e

Automatic container restarts
  docker run --restart=always --name daemon_container -d ubuntu /bin/sh -c "while true; do echo hello world; sleep 1; done"
  (docker will try to restart the container no matter what exit code is returned)
  --restart=on-failure:5 (this will attempt to restart the container a maximum of 5 times if a non-zero exit code is received)
  
Finding more about our container
  docker inspect daemon_container
  docker inspect --format='{{ .State.Running }}' daemon_container
  docker inspect --format '{{ .HostnamePath }}' daemon_container
  docker inspect --format '{{ .Name }} {{ .HostnamePath }}' daemon_container
  list multiple containers
    docker inspect --format '{{ .Name }} {{ .HostnamePath }}' daemon_container dameon_cont_2

Pulling images
  docker pull ubuntu
  docker pull fedora
  docker pull fedora:21
  docker pull jamtur01/puppetmaster

Searching for images
  docker search puppet

Sign into the Docker Hub
  docker login
  
Using Docker commit to create images
  Create a container from the ubuntu image
    docker run -i -t ubuntu /bin/bash
  Install Apache into the container
    apt-get -yqq update
    apt-get -y install apache2
  exit from the container 
    docker commit 6b84282435f8 dvdoc/apache2
    or
    docker commit -m="A new custom image" --author="DV Suresh" \
    6b84282435f8 dvdoc/apache2:webserver

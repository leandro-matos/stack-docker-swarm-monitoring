### Subindo um nginx simples

* docker stack deploy -c docker-compose.yml webserver-nginx
* curl 0:8080
* docker service ls
* docker service ps webserver-nginx_web
* docker stack ls
* docker stack services webserver-nginx
* docker stack ps webserver-nginx
* docker stack rm webserver-nginx

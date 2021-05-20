### Subindo um Wordpress com Banco de Dados Mysql

* docker stack deploy -c docker-compose.yml wordpress
* docker stack ls
* docker stack services wordpress
* docker service ls
* docker service ps wordpress_db
* docker service ps wordpress_wordpress
* docker service logs wordpress_wordpress

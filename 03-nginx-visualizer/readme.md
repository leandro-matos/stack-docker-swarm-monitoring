### Nginx com uma página de visualização do Cluster
* docker stack deploy -c docker-compose.yaml nginx-visualizer
* docker stack ls
* docker stack services nginx-visualizer
* docker service ls
* docker service logs nginx-visualizer_web

Visualizar a página do Visualizer:
http://IP_CLUSTER:8088/

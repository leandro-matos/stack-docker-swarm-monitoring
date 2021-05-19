1)
# docker stack deploy -c docker-compose.yml primeiro
# curl 0:8080
# docker service ls
# docker service ps primeiro_web
# docker stack ls
# docker stack services primeiro
# docker stack ps primeiro
# docker stack rm primeiro


2)
# docker stack deploy -c docker-compose.yml segundo
# docker stack ls
# docker stack services segundo
# docker service ls
# docker service ps segundo_db
# docker service ps segundo_wordpress
# docker service logs segundo_wordpress

3)
# docker stack deploy -c docker-compose.yml segundo
# docker stack ls
# docker stack services segundo
# docker service ls
# docker service ps segundo_db
# docker service ps segundo_wordpress
# docker service logs segundo_wordpress


4)
# docker stack deploy -c docker-compose.yml quarto
# docker service ls

Visualizar a página de votação:
http://IP_CLUSTER:5000/

Visualizar a página de resultados:
http://IP_CLUSTER:5001/

Visualizar a página de com os containers e seus nodes:
http://IP_CLUSTER:8080/

5)
# docker stack deploy -c docker-compose.yml giropops
# docker service ls 
# docker stack ls

Prometheus:
http://SEU_IP:9090

AlertManager:
http://SEU_IP:9093

Grafana:
http://SEU_IP:3000

Node_Exporter:
http://SEU_IP:9100

Rocket.Chat:
http://SEU_IP:3080

cAdivisor:
http://SEU_IP:8080

# docker stack rm giropops



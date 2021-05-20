### Deploy da Stack de Monitoring incluindo Grafana, Prometheus, NodeExporter
* docker stack deploy -c docker-compose.yml giropops
* docker service ls 
* docker stack ls

Prometheus:
**http://SEU_IP:9090**

Grafana:
**http://SEU_IP:3000**

Node_Exporter:
**http://SEU_IP:9100**

cAdivisor:
**http://SEU_IP:8080**

* docker stack rm giropops

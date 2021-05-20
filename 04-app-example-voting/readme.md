### Deploy da Aplicações de exemplo fornecidos pela Docker

* docker stack deploy -c docker-compose.yml microservices
* docker service ls

Visualizar a página de votação:
**http://IP_CLUSTER:5000/**

Visualizar a página de resultados:
**http://IP_CLUSTER:5001/**

Visualizar a página de com os containers e seus nodes:
**http://IP_CLUSTER:8080/**


# Comandos principais para gerenciamento do Docker Swarm

### Criação do Cluster e adicionando nós
docker swarm init
docker swarm join --token \ SWMTKN-1-100_SEU_TOKEN *SEU_IP_MASTER*:2377

### Listando os Nodes e exibindo os Tokens
docker node ls
docker swarm join-token manager
docker swarm join-token worker
docker swarm join-token --rotate manager **(Troca o token do Cluster)**

### Inspeciando o Node e promovendo para manager e rebaixando para worker
docker node inspect *node*
docker node promote *node*
docker node demote  *node*

### Removendo dos cluster
docker swarm leave
docker swarm leave --force
docker node rm *node*

### Criando um service Nginx com 05 replicas e exibindo detalhes dos mesmo
docker service create --name webserver --replicas 5 -p 8080:80  nginx
curl QUALQUER_IP_NODES_CLUSTER:8080
docker service ls
docker service ps webserver
docker service inspect webserver
docker service logs -f webserver
docker service rm webserver

### Detalhes sobre atualização dos Nodes
docker node update --availability pause indexer02 **(O nó não pode mais receber containers)**
docker service scale webserver=04
docker node update --availability active indexer02 **(O nó volta a receber containers)**
docker node update --availability drain indexer02
docker service rm webserver
docker service ls webserver

### Criando um service nginx com volume e rede overlay
docker service create --name webserver --replicas 5 -p 8080:80 --mount type=volume,src=teste,dst=/app  nginx
docker network create -d overlay webserver-nginx
docker network ls
docker network inspect webserver-nginx
docker service scale webserver-nginx=5
docker network rm webserver-nginx
docker service create --name webserver --network webserver-nginx --replicas 5 -p 8080:80 --mount type=volume,src=teste,dst=/app  nginx
docker service update <OPCOES> <Nome_Service> 
docker service inspect webserver-nginx --pretty **(Informação mais limpa na tela)

### Criação Simples de Volume
docker create volume webserver-nginx
docker service create --name webserver-nginx --replicas 3 -p 8080:80 --mount type=volume,src=webserver-nginx,dst=/usr/share/nginx/html nginx

### Compartilhamento de volume utilizando nfs-server (Método não muito recomendado):
apt-get install nfs-server
Editar arquivo */etc/exports* e incluir */var/lib/docker/volumes/webserver-nginx *(rw,sync,subtree_check)*
Rodar o comando *exportfs -ar*

### Nos clientes utilizar:
apt-get install nfs-utils
show mount -e 192.168.100.50
mount -t nfs 192.168.100.50:/var/lib/docker/volumes/webserver-nginx /var/lib/docker/volumes/webserver-nginx

### Criando o Service com Mais Opções:
docker service create --name webserver-nginx --replicas 3 -p 8080:80 --mount type=volume,src=webserver-nginx,dst=/usr/share/nginx/html --hostname splunkube --limit-cpu 0.25 --limit-memory 64M --env splunkube=prod nginx




# Comandos principais para gerenciamento do Docker Swarm

### Criação do Cluster e adicionando nós
* docker swarm init
* docker swarm join --token \ SWMTKN-1-100_SEU_TOKEN *SEU_IP_MASTER*:2377

### Listando os Nodes e exibindo os Tokens
* docker node ls
* docker swarm join-token manager
* docker swarm join-token worker
* docker swarm join-token --rotate manager **(Troca o token do Cluster)**

### Inspeciando o Node e promovendo para manager e rebaixando para worker
* docker node inspect *node*
* docker node promote *node*
* docker node demote  *node*

### Removendo dos cluster
* docker swarm leave
* docker swarm leave --force
* docker node rm *node*

### Criando um service Nginx com 05 replicas e exibindo detalhes dos mesmo
* docker service create --name webserver --replicas 5 -p 8080:80  nginx
* curl QUALQUER_IP_NODES_CLUSTER:8080
* docker service ls
* docker service ps webserver
* docker service inspect webserver
* docker service logs -f webserver
* docker service rm webserver

### Detalhes sobre atualização dos Nodes
* docker node update --availability pause indexer02 **(O nó não pode mais receber containers)**
* docker service scale webserver=04
* docker node update --availability active indexer02 **(O nó volta a receber containers)**
* docker node update --availability drain indexer02
* docker service rm webserver
* docker service ls webserver

### Criando um service nginx com volume e rede overlay
* docker service create --name webserver --replicas 5 -p 8080:80 --mount type=volume,src=teste,dst=/app  nginx
* docker network create -d overlay webserver-nginx
* docker network ls
* docker network inspect webserver-nginx
* docker service scale webserver-nginx=5
* docker network rm webserver-nginx
* docker service create --name webserver --network webserver-nginx --replicas 5 -p 8080:80 --mount type=volume,src=teste,dst=/app  nginx
* docker service update <OPCOES> <Nome_Service> 
* docker service inspect webserver-nginx --pretty **(Informação mais limpa na tela)

### Criação Simples de Volume
* docker create volume webserver-nginx
* docker service create --name webserver-nginx --replicas 3 -p 8080:80 --mount type=volume,src=webserver-nginx,dst=/usr/share/nginx/html nginx

### Compartilhamento de volume utilizando nfs-server (Método não muito recomendado):
1. apt-get install nfs-server
2. Editar arquivo */etc/exports* e incluir */var/lib/docker/volumes/webserver-nginx *(rw,sync,subtree_check)*
3. Rodar o comando *exportfs -ar*

### Nos clientes utilizar:
4. apt-get install nfs-utils
5. show mount -e 192.168.100.50
6. mount -t nfs 192.168.100.50:/var/lib/docker/volumes/webserver-nginx /var/lib/docker/volumes/webserver-nginx

### Criando o Service com Mais Opções:
* docker service create --name webserver-nginx --replicas 3 -p 8080:80 --mount type=volume,src=webserver-nginx,dst=/usr/share/nginx/html --hostname splunkube --limit-cpu 0.25 --limit-memory 64M --env splunkube=prod nginx

### Criação, Edição e Listagem de Secrets
* echo -n "Leandro Matos" | docker secret create leandro -
* docker secret ls
* docker secret inspect leandro
* docker secret create leandro-arquivo teste.txt
* docker secret rm leandro
* docker service create --name nginx -p 8080:80 --secret leandro-arquivo nginx
* docker service scale nginx=3
* docker service update --secret-add leandro nginx
* docker service create --name nginx2 -p 8081:80 --secret src=leandro-arquivo,target=meu-secret,uid=200,gid=200,mode=0400 nginx

### Mais um exemplo utilizando Secrets
* echo 'minha secret' | docker secret create 
* docker secret create minha_secret minha_secret.txt
* docker secret inspect minha_secret
* docker secret ls
* docker secret rm minha_secret
* docker service create --name app --detach=false --secret db_pass  minha_app:1.0
* docker service create --detach=false --name app --secret source=db_pass,target=password,uid=2000,gid=3000,mode=0400 minha_app:1.0
* ls -lhart /run/secrets/
* docker service update --secret-rm db_pass --detach=false --secret-add source=db_pass_1,target=password app

## Exemplos de Utilização do docker stack
* docker stack deploy -c docker-compose.yaml webserver-nginx
* docker stack ls
* docker stack ps webserver-nginx
* docker stack rm webserver-nginx
* docker service logs -f webserver-nginx
* docker node update --label-add dc=SP indexer02
* docker service scale webserver-nginx_web=8

*Portas de Comunicação do Swarm: 2377 TCP, 7946 TCP/UDP, 4789 UDP*


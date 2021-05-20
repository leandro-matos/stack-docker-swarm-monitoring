### Exemplos de Configuração com o Traefik
* Dentro do Arquivo de Configuração `webservers.yaml` incluir o domínio, nesse exemplo está o **observability.com.br**
* Após aplicar as configurações, no provedor onde registrou o domínio basta realizar os apontamentos para os IP's dos EC2
* Acessar os endereços e também a porta 8080 para Acesso ao Dashboard do Traefik

Nginx:   `https://loja.observability.com.br`
Apache:  `https://store.observability.com.br`
Traefik Dashboard: `http://SEU_IP:8080`

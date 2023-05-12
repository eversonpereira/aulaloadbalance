# Aula demonstrando load balance com nginx

Foi criado duas pastas myapp com um index.html estático e um Dockerfile para subir o container, um index retornando Hello World 1 e a outro Hello World 2.

Para facilitar utilizamos o docker-compose.

Foi criar um YML onde já sobe os dois containers web e um container com o nginx como load balancer.

O docker-compose.yml por padrão monta o arquivo nginx.conf como o arquivo de configuração do container do nginx LB.

No nginx.conf ele trabalha como Round Robin.

Criei dois outros arquivos de configuração, nginx-ha.conf e nginx-least-conn.conf

No nginx-ha.conf ele funciona como High availability, ou seja, ele só trocará para o segundo server se o primeiro estiver fora.

No nginx-least-conn.conf ele funciona como Least Connections, ou seja, enviará a nova solicitação para quem tem menos conexões.

No nginx-ip-hash.conf ele funciona como IP Hash, ou seja, agora irá utilizar o algoritmo IP Hash para distribuir o tráfego entre os servidores web, baseado no endereço IP do cliente.

No nginx-proxy-protocol.conf ele funciona como IP Hash, ou seja, agora está configurado para receber o protocolo Proxy Protocol, que permite a identificação do endereço IP real do cliente que está acessando o servidor web.

Basta trocar na linha 16 do docker-compose.yml para a configuração desejada, por exemplo para utilizar o ha deverá mudar essa linha de:
./nginx.conf:/etc/nginx/nginx.conf
para
./nginx-ha.conf:/etc/nginx/nginx.conf

Para inicializar o exemplo, com o docker e o docker compose instalado na pasta raiz do projeto executar docker-compose up

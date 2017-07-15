### Rede no Docker


1. Crie um novo container nginx: `docker run -d --name teste nginx:alpine`;
2. Verifique o endereço IP através do comando: `docker inspect teste`;

> Por padrão o Docker, através da ***Docker Bridge***, fornece um endereço IP para os containers, mas que não pode ser acessado por ambientes externos.  

> Para acessar um container(processo) pelo ambiente externo é necessário mapear uma porta entre host e container.  
Isso é feito através do parâmetro `-p` do comando `docker run`.

`docker run -d -p 8080:80 --name teste nginx:alpine`

> Para gerar uma porta aleatória use o parâmetro `-P` em caixa alta.

`docker run -d -P --name teste nginx:alpine`


----------------------------------------------------------------------------
### Tratando Logs
----------------------------------------------------------------------------

O Docker possui um recurso para visualizar os logs de saída e de erro padrão `( stdout e stderr )`.  

Isso é interessante para verificarmos o que está acontecendo dentro de um container, sem a necessidade de conferir um determinado arquivo de log.  

Para este exemplo, vamos utilizar o `DOCKERFILE` e redirecionar os logs do Nginx para `stdout` e `stderr`.  
O `DOCKERFILE` ficará assim:  

```sh
FROM ubuntu
MAINTAINER Beltrano Dias <beltrano@email.com>
RUN apt-get update
RUN apt-get install -y nginx
ADD exemplo /etc/nginx/sites/enabled/default
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

`$ sudo docker build -t nginx .`

`$ sudo docker run -d -p 80:80 --name teste nginx`

Faça alguns requests para gerar registros nos logs:  


`$ for ( (i-1; i<-10; i++) ); do curl -IL http://127.0.0.1; done`

Agora, podemos conferir os logs utilizando o comando `docker logs` e a identificação do nosso container:


`docker logs teste`


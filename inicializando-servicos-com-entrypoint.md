----------------------------------------------------------------------------
### Inicializando Serviços
----------------------------------------------------------------------------

Podemos reduzir o comando utilizado para geração de containers, informando no `Dockerfile` a instrução `CMD`.  
Isso será feito para que se possa inicializar um serviço, no caso o Nginx, sempre que um container novo for criado. Vamos ao exemplo:

```sh
FROM ubuntu
MAINTAINER Sicrano da Silva <sicrano@email.com>
RUN apt-get update
RUN apt-get install -y nginx
ADD exemplo /etc/nginx/sites/enabled/default
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
ADD ./ /rails
WORKDIR /rails
EXPOSE 8080
CMD service nginx start
```

Existe outra forma de inicializar serviços, utilizando `ENTRYPOINT`.  

Sempre que usamos `CMD` em seu background, ele está chamando o bash assim:  

`/bin/sh -c`

Em seguida, envia como parâmetro o comando ou instrução que especificamos.  

A diferença em usar `ENTRYPOINT` é que ele chama o comando ou script diretamente, por exemplo:  

```sh
...
EXPOSE 8080
ENTRYPOINT ["/usr/sbin/nginx"]
```

Quando utilizamos `ENTRYPOINT` , tudo o que for especificado em `CMD` será enviado como complemento para `ENTRYPOINT`:

```sh
...
ENTRYPOINT ["/etc/init.d/nginx"]
CMD ["start"]
```


```sh
FROM ubuntu
MAINTAINER Sicrano da Silva <sicrano@email.com>
RUN apt-get update
RUN apt-get install -y nginx
ADD exemplo /etc/nginx/sites/enabled/default
RUN echo "daemon off;" >> /etc/nginx/nginx.conf
ADD ./ /rails
WORKDIR /rails
EXPOSE 8080
ENTRYPOINT ["/etc/init.d/nginx"]
CMD ["start"]
```

Recrie a imagem, inicialize um container:

```sh
$ sudo docker build -t nginx .

$ sudo docker run -d nginx
```

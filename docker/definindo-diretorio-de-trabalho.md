
----------------------------------------------------------------------------
### Definindo o diretório de trabalho
----------------------------------------------------------------------------

A área de trabalho padrão do Docker é o diretório raiz `/`.  

Podemos alterar isso durante a criação de um container ao usarmos a opção `-w` , ou tornando
padrão usando a diretiva `WORKDIR` no `DOCKERFILE`.  

Imagine que queremos utilizar um container para desenvolvimento de um projeto Ruby on Rails.  
O `DOCKERFILE` poderia ser adicionado dentro do diretório do projeto e teria as seguintes configurações:

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

Com o diretório de trabalho definido em `WORKDIR` , temos antes dele o `ADD ./ /rails`, que copia os arquivos a partir do contexto no qual foi executado para o filesystem do container.  

Lembre-se de que este arquivo `DOCKERFILE`, neste exemplo, está dentro do projeto Rails:

```sh
$ rails new docker_example

$ cp DOCKERFILE docker_example/

$ cd docker_example

$ sudo docker build -t nginx .
```

Com a nova imagem gerada, vamos criar um novo container:  

`$ sudo docker run -d -p 8080:8080 --name app nginx`

Basicamente agora a área de trabalho principal dentro deste container é a própria aplicação Rails.  
Desta forma, poderíamos usar este container como ambiente de desenvolvimento.  

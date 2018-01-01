

#### Expondo e mapeando portas

```sh
FROM ubuntu
MAINTAINER Fulano de Tal <fulano@email.com>
RUN apt-get update
RUN apt-get install -y nginx
EXPOSE 80
```

* EXPOSE

>* Usado para informar qual porta o container docker irá `"escutar"`. 
>* Docker usa essa informação para interconexão entre containers, ao utilizar links.

>* `EXPOSE` **não define** qual porta será exposta para o hospedeiro, ou tornar possível o acesso externo para portas do container em questão.
>* Para expor essas portas utilize em tempo de inicialização da imagem a flag `-p` ou `-P`.

* Execute o comando para criar a imagem.

`sudo docker build -t imagemteste .`

Agora, podemos testar criando uma nova instância:

`sudo docker run -d -P --name teste imagemteste /usr/sbin/nginx -g "daemon off;"`

>* Ao criar um container passando a instrução `-P` , estamos permitindo que o Docker faça o mapeamento de qualquer porta utilizada no container, 
para alguma outra porta no host. 
>* Conferiremos isso com o `docker ps` , ou usando o seguinte atalho:

`sudo docker port teste`


>* Ou podemos utilizar especificando a porta do container:

`sudo docker port teste 80`

Sempre que um container for criado desta forma, o retorno da instrução `-P` será uma porta aleatória criada no host.



#### Adicionando arquivos ao container

Imagine se você precisar fazer várias alterações nos arquivos de configuração de um web server,
a produtividade pode ser comprometida.  

>Para resolver isso, vamos utilizar a opção `ADD` no `DOCKERFILE`.  


Desta forma, vamos referenciar o arquivo que queremos copiar e o local de destino para a imagem durante o processo de build.  

```sh
FROM ubuntu
MAINTAINER Beltrano <beltrano@email.com>
RUN apt-get update
RUN apt-get install -y nginx
ADD exemplo /etc/nginx/sites-enable/default
EXPOSE 8080
```

Com a instrução `ADD` , o arquivo chamado exemplo será copiado para o diretório `/etc/nginx/sites-enabled` ,
e será chamado de `default`.  

O arquivo `exemplo` deve existir no mesmo contexto(diretório) do `DOCKERFILE`.  
O seu conteúdo é bem simples e foi alterado apenas para o Nginx utilizar a nova porta, no nosso caso, a `8080`.  

```sh
server {
  listen 8080 default_server;
  server_name localhost;

  root /usr/share/nginx/html;
  index index.html index.htm;
}
```

Agora, podemos executar o nosso processo de build e gerar a nova imagem.  
O arquivo será copiado para as configurações do Nginx:  

`sudo docker build -t nome_imagem .`

Então, vamos criar um novo container, sem informar instruções de portas, e testar para ver se está tudo certo: 

`sudo docker run -d nome_imagem /usr/sbin/nginx -g "daemon off;"`

Como resposta, recebemos um erro em nosso teste.  
Será que esquecemos alguma coisa?  
Não, não esquecemos de nada.  


>Quando utilizamos o `-p` ou o `-P` , estamos mapeando uma porta **interna do container** para uma porta em nosso **host local**.  

Agora verificaremos o funcionamento do Nginx acessando o diretamente o IP do container.

Para capturar informações do container, podemos fazer uso da opção `inspect`, que retorna informações low-level de um container, ou de uma imagem.  

`sudo docker inspect id_imagem`

ou filtrando:  

`sudo docker inspect | grep IPAddress`

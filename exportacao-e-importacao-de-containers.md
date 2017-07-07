
----------------------------------------------------------------------------
### Exportação e Importação de Containers
----------------------------------------------------------------------------

Imagine que temos um container em execução e queremos exportá-lo para outro host.  

Outra situação parecida é um container funcionando __localmente__, porém queremos levá-lo para um host em __produção__.  

Podemos criar uma imagem partindo de um container que está **funcionando**, e gerar um arquivo `.tar` usando a opção `save`.  

Para criar a nova imagem, basta fazer um `commit` no container em execução:  

`$ sudo docker ps -q`

`$ sudo docker commit e20af9875148 nova_imagem`

De posse da nova imagem que foi gerada, faremos a exportação criando um arquivo:  

`$ sudo docker save nova_imagem > /tmp/nova_imagem.tar`

Agora o arquivo `.tar` que foi criado pode ser enviado para o outro host, via `SCP` , por exemplo.  
Para fazer a importação desse arquivo, utilizamos a opção `load`:  

`$ sudo docker load < /tmp/nova_imagem.tar`

Este fluxo pode ser usado em operações para projetos privados.  


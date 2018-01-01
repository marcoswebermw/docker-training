----------------------------------------------------------------------------
### Gerenciamento de recursos Docker
----------------------------------------------------------------------------


#### Comitando containers em novas imagens

* Toda alteração em um container é volátil. Tudo se perde a não ser se a alteração for commitada.

`sudo docker commit nomedocontainer nomedanovaimagem/versao`

* Ao executar o commit será criada uma nova imagem baseada na inicial com o nome de `nomedanovaimagem/versao`.


#### Container em background
* Usando o `-d` mandamos o container direto para background:

`sudo docker run -d -p 8080:80 ubuntu/nginx /usr/sbin/nginx -g`

* Verifique com o comando abaixo se o container está rodando.

`sudo docker ps -q`


#### Manipulando a execução do container

* Agora vamos manipular seu funcionamento com start e stop. Para isso, basta indicar o nome do container ou seu id:

`sudo docker stop nome_ou_id_do_container`

`sudo docker start nome_ou_id_do_container`


>* Note que, ao executar o stop, quando verificamos se o processo que faz referência ao container existe, nada é retornado. Isso acontece, pois o processo está em pausa.


#### Acessando um container

* Para entrar direto em um container em execução use:

`sudo docker attach container_de_teste`

* Para executar um determinado comando ou entrar no container, como feito pelo docker attach, use o exec:

`sudo docker exec -t -i nome_container /bin/bash`

`sudo docker exec nome_container cat /etc/lsb-release`


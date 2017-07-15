### Volumes

> Volumes são usados para armazenar dados de forma que estes fiquem disponíveis para serem usados em outros containers.
Os dados não ficam limitados ao container atual.

##### Criando volumes

`docker volume create meu_volume`

##### Listando todos os volumes

`docker volume list`


##### Montando um volume dentro de um container

> Será necessário usar o parâmetro `-v` com o comando `docker run`.

`docker container run -it -v meu_volume:/local_de_montagem ubuntu bash`

##### Exemplo de criação e uso de volumes:

* Crie um volume: `docker volume create meu_volume`;
* Verifique se o volume foi criado: `docker volume list`;
* Crie um container montando nele o nosso volume criado: `docker run -it -v meu_volume:/dados_salvos alpine sh`;
* Crie alguns arquivos dentro desse volume: `cd /dados_salvos && touch arquivo1 arquivo2 && exit`;
* Agora crie um novo container e monte nosso volume: `docker run -it -v meu_volume:/dados_salvos busybox sh`;
* Então verifique que os arquivos criados no outro container permanecem no volume: `ls /dados_salvos`.  

> Volumes são muito úteis quando precisamos compartilhar arquivos entre vários containers. Como exemplo podemos citar os arquivos de um banco de dados que precisem ser acessado por diversos containers.

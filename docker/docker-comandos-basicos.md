---------------------------------------------------
## DOCKER: COMANDOS BÁSICOS
---------------------------------------------------


#### VERIFICAR AS IMAGENS BAIXADAS
```sh
docker images
```
---------------------------------------------------
#### ATUALIZAR UMA IMAGEM BAIXADA
```sh
docker pull hello-world
```
---------------------------------------------------
#### DESCOBRINDO TODOS OS DADOS DE UMA IMAGEM
```sh
docker inspect hello-world
```
---------------------------------------------------
#### RODANDO COMANDOS NO DOCKER

> docker run <parâmetros> <imagem> <CMD[shell]> <argumentos>

```sh
EX.: docker run -it --rm --name ola_mundo hello-world bash
```
```sh
EX.: docker run -it --rm -v /home/$USER/meu_volume:/meu_volume -e USER=$USER -w /meu_volume  ubuntu bash
```
---------------------------------------------------

| Parâmetro | Explicação|
| --------- | --------- |
|         |                                        |
|   -c    | Balanceia o uso de CPU.                |
|   -d    | Execução do container em background.   |
|   -e    | Define uma variável de ambiente para o container. |
|   -h    | Define o nome de host para o container. |
|   -i    | Modo interativo.                       |
|   -m    | Limita a memória RAM.                  |
| --name  | Dá um nome para o container.           |
|   -p    | Mapeia a porta.                        |
|  --rm   | Remove o container após a finalização. |
|   -t    | Aloca um pseudo TTY.                   |
| --user  | Define o usuário do container. (Usuário deve existir no container). |
|   -v    | Mapeia o volume.                       |
|   -w    | Diretório de trabalho inicial.         |

> O parâmetro '--rm' não funciona quando for usado o '-d'.

---------------------------------------------------
#### MAPEANDO UMA PORTA
```sh
docker run -it --rm -p 80:8080 hello-world 
```
* Toda requisição para a porta 80 do host seria encaminhada para a porta 8080 do container.\
* Não será possível acessar diretamente a porta 8080 do container.

---------------------------------------------------
#### LIMITANDO A RAM DO CONTAINER
```sh
docker run -it -rm -m 512M hello-world bash
```
> O container só poderá usar 512MB de RAM.

---------------------------------------------------
#### LIMITANDO O USO DE CPU

 * Isso é feito por prioridade de 1 a 1024. 1024 é o padrão e a prioridade máxima.
 * Quanto mais prioridade um container tiver, mais tempo poderá usar a CPU antes de outros.
```sh
docker run -it --rm -c 512 hello-world
```
---------------------------------------------------
#### VERIFICANDO A LISTA DE CONTAINERS
```sh
docker ps
```

 | Parâmetro | Explicação|
 | --------- | --------- |
 | -a | Todos os containers mesmo os desligados.|
 | -l | Lista os ultimos containers, inclusive os desligados.|
 | -n | Lista os ultimos n containers, mesmo os desligados.|
 | -q | Lista apenas os ids dos containers.|
 |  |Sem qualquer parâmetro o 'ps' mostrará apenas os containers que estão rodando.|

```sh
docker ps -aq
```
---------------------------------------------------
#### GERENCIAMENTO DE CONTAINERS

> Para desligar o container use o 'stop' seguido do nome ou id do container.
```sh
docker stop hello-world
```

 > 1. __Para reiniciar um container sem criar um novo basta usar o 'start'.__
 > 2. __Os containers do docker foram feitos para executar como processos.__
 > 3. __Então é melhor sempre destruir e criar novos processos ao invés de usar um container antigo.__
 > 4. __Isso já é feito quando usado o parâmetro '--rm'.__
 > 5. __Lembrando que 'containers' são processos e são diferentes de imagens.__

```sh
docker start hello-world
```
---------------------------------------------------
#### REMOVENDO IMAGENS E CONTAINERS(PROCESSOS)

> Removendo um container:
```sh
docker rm nome_ou_id_do_container
```
 
> Removendo todos os containers:
```sh
docker rm $(docker ps -qa)
```


> Removendo uma imagem:
```sh
docker rmi nome_ou_id_da_imagem
```
> Removendo todas as imagens:
```sh
docker rmi $(docker images -q)
```

---------------------------------------------------
### DOCKER: COMANDOS BÁSICOS
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
```sh
docker run <parâmetros> <imagem> <CMD[shell]> <argumentos>
```

>EX.: docker run -it --rm --name ola_mundo hello-world bash

---------------------------------------------------

| Parâmetro | Explicação|
| --------- | --------- |
|         |                                        |
|   -d    | Execução do container em background.   |
|   -i    | Modo interativo.                       |
|   -t    | Aloca um pseudo TTY.                   |
|  --rm   | Remove o container após a finalização. |
| --name  | Dá um nome para o container.           |
|   -v    | Mapeia o volume.                       |
|   -p    | Mapeia a porta.                        |
|   -m    | Limita a memória RAM.                  |
|   -c    | Balanceia o uso de CPU.                |

>O parâmetro '--rm' não funciona quando for usado o '-d'.

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
>Parâmetros:

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

 * __Para reiniciar um container sem criar um novo basta usar o 'start'.__
 * __Os containers do docker foram feitos para executar como processos.__
 * __Então é melhor sempre destruir e criar novos processos ao invés de usar um container antigo.__
 * __Isso já é feito quando usado o parâmetro '--rm'.__
 * __Lembrando que 'containers' são processos e são diferentes de imagens.__

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

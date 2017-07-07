-----------------------------------------------------------
### CRIANDO IMAGENS NO DOCKER
-----------------------------------------------------------

> + Os nomes da imagem seguem um padrão: `repositório:tag`
>   - Ex.: `ubuntu:16.04` ou `ubuntu:14.04`

> + Existem duas formas de criar imagens no docker: com commit ou Dockerfile.

#### CRIANDO IMAGENS COM DOCKERFILE

>* O `DOCKERFILE` é um arquivo que informa como será criada uma nova imagem com base em outra.
>* É um recurso feito para automatizar o processo de execução de tarefas no docker.
>* Com este recurso, podemos descrever o que queremos inserir em nossa imagem.
>* Quando geramos um `build` , o Docker cria um snapshot com toda a instalação que elaboramos no `DOCKERFILE`.
>* O `DOCKERFILE` é um arquivo que aceita rotinas em shell script para serem executadas.


Exemplo de um Dockerfile:

* Para exemplo crie um arquivo 'ola.txt'.
* Depois crie o arquivo abaixo e dê o nome de Dockerfile.

---------------------------------------------------
```sh
FROM ubuntu:16.04
MAINTAINER Fulano de Tal <fulano@email.com>
RUN apt update && apt install nginx -y
RUN cd ~ && mkdir novo_diretorio
RUN rm -rf novo_diretorio
COPY ola.txt /tmp/ola.txt
CMD bash
```
---------------------------------------------------

Explicação:

| Comando | Explicação |
| ---------- | ---------- |
|   FROM   | Imagem usada como base para a nova. |
|   MAINTENER   | Responsável por manter a imagem.|
|   RUN   | Comandos que serão executados dentro do container. |
|   COPY   | Arquivo será copiado do host para dentro do container. |
|   CMD   | Comando executado por padrão caso nenhum seja dado na criação do container. |

> Para gerar a nova imagem com base na outra digite o seguinte comando:

```sh
docker build -t minha_nova_imagem:versao .
```

* O parâmetro `-t` indica um nome ou tag no formato 'nome:tag' para a build. No caso será `'minha_nova_imagem:versao'`.
* O parametro -t é para dar .
* Repare o ponto(`.`) no final. Ele indica o contexto(diretório) que será usado para gerar a imagem.
* Isso significa que no caso com o `'.'` todos os arquivos do diretório atual poderão ser usados dentro do container, que é o que ocorre com o arquivo `'ola.txt'` usado com o `'COPY'`.
* Nenhum outro arquivo de outro diretório poderá ser reaproveitado aqui.

* A ordem em que os comandos são executados importa. Todo comando que depende de outro deve vir depois da dependência.
* Se houver uma modificação o docker vai usar um cache e só vai executar os comandos a partir do que foi modificado.
* Assim, deixando a execução mais rápida do que se tivesse que fazer a operação desde o começo.


---------------------------------------------------


## Instruções usadas no `Dockerfile`

> O exemplo de `Dockerfile` no final do arquivo demonstra o uso dessas instruções.

-------------------------

#### ARG

* A instrução `ARG` define uma **variável** que é passada em tempo de construção(build) para a imagem pelo comando `docker build`. 
É passada através do parâmetro `--build-arg`. Uma ou mais variáveis podem ser criadas com `ARG`.

-------------------------
#### USER  

* A instrução `USER` colocada no arquivo Dockerfile define que os comandos a partir dali serão executados com privilégios de acordo com o usuário(UID) ou grupo(GID) passados.
Esta instrução tem efeitos sobre instruções como RUN, CMD e ENTRYPOINT.



-------------------------
##### Exemplo de Dockerfile

```
FROM python:3.5

# Usuário passado na hora do build da imagem.
ARG usuario

# Instalando dependências e fazendo algumas configurações.
RUN apt update && apt install -y \
    vim \
    git \
    && pip install --upgrade pip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Copiando os arquivos do diretório atual do host para o diretório /install do container.
ADD ./ /install

# Instalando dependências.
RUN pip install --no-cache-dir -r /install/requirements.txt

# Criando usuário no sistema e dando permissões no diretório criado.
RUN useradd $usuario \
    && usermod -G root $usuario \
    && mkdir -p /home/$usuario/minha-app \
    && chown -R $usuario:$usuario /home/$usuario/minha-app

# Definindo diretório de trabalho padrão.
WORKDIR /usr/src/minha-app

# Trocando o usuário logado.
USER $usuario

# Executando o bash.
CMD [ "bash" ]

```

* Depois o comando de build da imagem passando argumento pelo parâmetro `--build-arg`:
```
docker build --build-arg usuario=$USER -t mw/minha-app .
```

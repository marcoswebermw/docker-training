-------------------------------------------------------------------------------------------
### INSTALANDO O DOCKER
-------------------------------------------------------------------------------------------


#### CONFIGURANDO O REPOSITÓRIO


> _Instalando dependências:_
```sh
sudo apt-get -y install apt-transport-https ca-certificates curl
```

> _Baixando chaves:_
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

> _Adicionando repositório:_
```sh
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

> _Atualizando repositório:_
```sh
sudo apt-get update
```


#### INSTALANDO A ÚLTIMA VERSÃO DO DOCKER CE PARA UBUNTU
```sh
sudo apt-get -y install docker-ce
```

#### TESTANDO A INSTALAÇÂO
```sh
sudo docker run hello-world
```

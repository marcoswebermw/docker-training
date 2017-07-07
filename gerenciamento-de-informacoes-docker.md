----------------------------------------------------------------------------
### Gerenciamento de informações
----------------------------------------------------------------------------


#### Problemas ao executar o docker:  

Se houver problema para rodar o docker, tente diminuir o `MTU` da rede para um valor __inferior__ a **1500**... talvez 1000 ou 900 resolva.  

---------------------------------------------------

#### Para ver a versão do docker:  

`sudo docker version`

#### Para ver informações do docker:  

`sudo docker info`

---------------------------------------------------

#### Comando stats

A partir da versão 1.5 o docker possui a feature `stats`, que informa, em tempo de execução, detalhes sobre o nível de consumo de recursos na máquina host, feito pelos containers.  

`sudo docker stats meu_container`

#### Comando top

Além do comando `stats` para estatísticas de uso do sistema, o docker também oferece o comando `top`:  

`sudo docker top nome_do_container`

---------------------------------------------------

#### Comando inspect

Descubra todos os dados de uma imagem:  

```sh
docker inspect hello-world
```
#### Comando logs

O `logs` retorna os logs de comando executados no container:  

`sudo docker logs nome_ou_id_do_conainer`



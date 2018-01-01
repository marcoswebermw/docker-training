-----------------------------------------------------------
### CRIANDO IMAGENS NO DOCKER
-----------------------------------------------------------

> + Os nomes da imagem seguem um padrão: `repositório:tag`
>   - Ex.: `ubuntu:16.04` ou `ubuntu:14.04`

> + Existem duas formas de criar imagens no docker: com commit ou Dockerfile.

#### CRIANDO IMAGENS COM COMMIT

* Baixe a imagem que servirá como base; 
* Faça as alterações necessárias em um container dela;
* grave as alterações feitas container em outra imagem com o comando `commit` seguido do nome da nova imagem.

> Ex.:

```sh
docker run -it --name novocontainer ubuntu:16.04 bash 
```

* Dentro do container instale os pacotes necessários:
 
 ```sh
 apt update && apt install nginx -y && exit
 ```

 * Depois vamos parar esse container e salvá-lo como uma nova imagem com o nginx instalado nela.

```sh
 docker stop novocontainer
 ```
```sh
 docker commit novocontainer meu_ubuntu_servidor_web:nginx
 ```

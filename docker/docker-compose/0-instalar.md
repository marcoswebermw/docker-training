# Instalando o Docker Compose  

1 - É necessário que o Docker Engine([Docker CE](https://docs.docker.com/install/#server)) esteja instalado.  
  
2 - Baixe o binário:  
  
 ```sh
 sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
 ```  
  
 3 - Dê as permissões de execução:  
   
  ```sh
  sudo chmod +x /usr/local/bin/docker-compose
  ```  
    
> Para garantir crie um link simbólico no diretório `/usr/bin`.  
  
```sh
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```  
  
4 - Testando  
  
 ```sh
 docker-compose --version
 ```  
   
5 - Desinstalando  
  
 ```sh
 sudo rm /usr/local/bin/docker-compose
 ```  
 
## Instalando o Comand-line Completion(Bash)  
  
```sh
sudo curl -L https://raw.githubusercontent.com/docker/compose/1.23.2/contrib/completion/bash/docker-compose -o /etc/bash_completion.d/docker-compose
```  
  
 > Mais em [Command-line completion](https://docs.docker.com/compose/completion/)  
   
## Referências  

[Docs Docker - Install ](https://docs.docker.com/compose/install/)    

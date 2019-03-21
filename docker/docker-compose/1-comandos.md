# Comandos Básicos do Docker Compose  

```sh
# Inicia os serviços.
docker-compose up

# Inicia os serviços em background.
docker-compose up -d

# Inincia os serviços, mas antes faz a reconstrução da imagem.
docker-compose up --build

# Para a execução dos serviços iniciados com `-d`, mas não elimina os processos(containers).
docker-compose stop

# Para a execução dos serviços, e elimina os processos.
docker-compose down

# Para a execução dos serviços, e elimina os processos. Além de remover volumes associados.
docker-compose down --volumes

# Executa comandos dentro de serviços em execução.
docker-compose run meu_servico env
docker-compose run meu_servico pwd
docker-compose run meu_servico ls
```  

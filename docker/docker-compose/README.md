# Docker-Compose  

- É uma ferramenta para criação e execução de aplicações divididas em múltiplos containers Docker;   
- Usa um arquivo YAML para configurar os serviços das aplicações - `docker-compose.yml`;  
- Através de um comando pode criar e iniciar vários containers de acordo com a configuração definida no arquivo `yml`;  
- Pode ser usado para trocar entre ambientes isolados para desenvolvimento, testes, produção, homologação, etc, tudo de forma rápida;  
- Facilita a criação de ambientes com integração contínua e entrega contínua;  
- É possível iniciar, parar, reconstruir serviços. E mesmo iniciar um serviço isoladamente;  
- Permite a visualização do status, verificar logs de serviços em execução;  
- Preserva os dados de volumes mesmo quando estes são encerrados;  
- Usa cache na criação de containers, e só faz rebuild quando necessário. Agilizando o processo.  

## Passos para usar o docker-compose  

1 - Criar um Dockerfile para definir o ambiente necessário;  
2 - Criar um docker-compose.yml indicando todos os serviços que irão executar em conjunto, só que em ambientes isolados;  
3 - Iniciar o ambiente com o comando `docker-compose up`


## Exemplo do `docker-compose.yml` tirado da documentação  

```yaml
version: '3'
services:
  web:
    build: .
    ports:
    - "5000:5000"
    volumes:
    - .:/code
    - logvolume01:/var/log
    links:
    - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```

## Referências  

[Docs Docker](https://docs.docker.com/compose/overview/)    

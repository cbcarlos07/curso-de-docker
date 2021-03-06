# Curso de docker
https://www.udemy.com/share/1001G2AEYedVtWRXo=/

## Repositório do curso

    https://github.com/cod3rcursos/curso-docker

## Para testar o docker
Para rodar container hello-docker
    
    $ docker containr run hello-world


Para ver o bash do debian

    $ docker container run -it debian bash 
    $ docker container run debian bash --version

Para dar criar container com nome

    $ docker container run --name mydeb -it debian bash    
    --name: nome do container
    --it: modo interativo

Para listar container
  
     $ docker container ls 
     $ docker container ls -a

Para verificar container ativos no momento

    $ docker container ps

Para mostrar os containers executados independente do status

    $ docker container ps -a

Para apagar o container após a execução

    $ docker container run --rm debian bash -version
  
Para reutilizar container
    
    $ docker container start -ai mydeb

Mapear porta 

    $ docker container run -p 8080:80 nginx

Mapear volume

    $ docker container run -p 8080:80 -v $(pwd)/not-found:/usr/share/nginx/html  nginx
    $ docker container run -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html  nginx
    $ docker container run -p 8080:80 -v $(pwd)/nomedapasta:/usr/share/nginx/html  nginx

Rodar servidor em background

    $ docker container run -d --name nome_do_container -p 8080:80 -v $(pwd)/html:/usr/share/nginx/html nginx
    -d: modo daemon ou seja background

Parar um container

    $ docker container stop nome_do_container

Restartar um container

    $ docker container restart nome_do_container

Para listar containers

    $ docker container ls
    $ docker container ls -a
    $ docker container ps
    $ docker container ps -a
    $ docker container list

Para ver os logs

    $ docker container logs nome_do_container
    $ docker container inspect nome_do_container
    $ docker container exec nome_do_container uname -or

Listas

    $ docker image ls
    $ docker volume ls
    $ docker container ls

Ajudas

    $ docker image --help
    $ docker container --help
    $ docker volume --help

## Entrar na pasta onde se localiza a imagem

Obter imagem do hub.docker.com Redis

    $ docker image pull redis:latest

Adicionar nova tag para a imagem    

    $ docker image tag redis:latest cod3r-redis
    $ docker image tag image:tag nova-tag

Remover imagem

    $ docker image rm redis-latest cod3r-redis

Formato Simples do Dockerfile # aula 35

    FROM nginx:latest
    RUN echo '<h1>Hello World</h1>' > usr/share/nginx/html/index.html

    FROM image:versao

Gerar imagem a partir do Dockerfile

    $ docker image build -t ex-simple-build .    
    -t = significa a tag que eu quero adicionar
    $ docker image build -t minha-tag .
    . = minha pasta atual

Para ver lista de imagem criada
    
    $ docker image ls

Executar container
    
    $ docker container run -p 80:80 ex-simple-build 
    -p 80:80=  para mapear a porta. Porta externa: porta interna

Mostrar o valor padrão de uma variável de ambiente
    
    $ docker container run ex-build-arg bash -c 'echo $S3_BUCKET'
    a chave é nomeada de S3_BUCKET

Gerar um novo container passando argumento para o S3_BUCKET a partir de outra imagem
    
    $ docker image build --build-arg S3_BUCKET=myapp -t ex-build-arg .

Acessar o inspect
    
    $ docker image inspect --format="{{index .Config.Labels \"maintainer\" }}" ex-build-arg

Para parar um container por ID
    
    $ docker container stop CONTAINER_ID
    Não esquecer de substituir o CONTAINER_ID pelo seu código de container

Enviar imagem para o hub.docler

    $ docker image tag ex-simple-build cbcarlos7/simple-build
    $ docker image tag ex-simple-build contaUsuario/tag

Logar no hub.docker.com

    $ docker login --username=cbcarlos7

Fazer o push da imagem

    $ docker image push cbcarlos7/simple-build:1.0
    $ docker image push usuario-hub/nome-da-imagem:versao


## Redes

Lista de modelos de rede

    $ docker network ls

Executar container sem rede

    $ docker container -d --net none debian
    -d: modo daemon
    --net: formato de rede
    none: sem rede
    debin: nome da imagem

Executar container e apagar logo após a execução

    $ docker container run --rm alpine ash -c "ifconfig"
    --rm: apaga o container logo após a execução
    alpine: nome da imagem
    ash: bash mais reduzido
    -c: irá ser especificado um comando
    "ifconfig": comando que será executado

Executar container e apagar logo após a execução sem rede

    $ docker container run --rm --net none alpine ash -c "ifconfig"
    --net: especifica se tem rede
    none: especifica que não tem rede

Inspecionar rede bridge

    $ docker network inspect bridge

Criar container em modo daemon

    $ docker container run -d --name container1 alpine sleep 1000
    --name: nome do container
    sleep: tempo de execução do container
    1000: ficar todo tempo em execução

Acessar o container criado

    $ docker container exec -it container1 ifconfig
    exec: executar o container
    -it: modo interativo, dentro do container criado
    container1: nome do container criado
    ifconfig: comando dentro do container

Executar comando de dentro de um container para o ip de outro container

    $ docker container exec -it container1 ping 172.17.0.3

Criar nova rede

    $ docker network create --driver bridge rede_nova

Criar container na rede nova criada

    $ docker container run -d --name container3 --net rede_nova alpine sleep 1000

Fazer um container de uma rede conectar a outra rede diferente

    $ docker network connect bridge container3
    Aqui o container3 que é faixa 172.18. vai conectar à rede da faixa 172.17. 

Desconectar container de uma rede

    $ docker network disconnect bridge container3

Usar um container na rede modo host

    $ docker container run -d --name container4 --net host alpine sleep 1000

## Composer

Após criar o arquivo docker-composer.yml para rodar é preciso dar o comando:

    $ docker-compose up

Iniciar docker compose em modo daemon

    $ docker-compose up -d

Rodar um comando dentro do serviço definido no docker-composer.yml 

    $ docker-composer exec db psql -U postgres -c '\l'
    '\l': Roda a lista de banco de dados

Parar o serviço do docker-compose.yml

    $ docker-compose down 

## Banco de dados

\l: Lista do banco de dados postgres

\c: conectar ao banco de dados

\d: Gerar descrição

Acessar o arquivo check.sql

    $ docker-compose exec db psql -U postgres -f script/check.sql
    exec: comando que vai ser executado
    db: nome do serviço definido no arquivo docker-compose.yml
    psql: comando do postgres
    -U: logo após será definido o usuário
    postgres: usuário do banco
    -f: arquivo que será executado

No docker-compose.yml

    a tag: depends_on: Se for inicializado somente um serviço, se esta tag estiver dispoível, o outro serviço também inicializará
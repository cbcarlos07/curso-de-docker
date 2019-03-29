# Curso de docker
https://www.udemy.com/share/1001G2AEYedVtWRXo=/

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
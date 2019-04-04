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

Verificar os logs

    $ docker-compose logs -f -t

Tag no docker-compose

    A tag build dentro do serviço refere-se à imagem definida no arquivo Dockerfile

Escalando container

    $ docker-compose up -d --scale worker=3

No arquivo docker-compose:

    A tag environment dentro do serviço é a possibilidade de personalizar variaveis de ambiente

Chamar o docker-compose baseado em configuracao de variáveis de ambiente producao ou simulacao

    docker-compose -f docker-compose.dev.yml up -d

    export COMPOSE_FILE=docker-compose.dev.yml
    docker-compose up -d

Docker apache, mysql, php
    
    https://gotechnies.com/docker-compose-yml-mysql-phpmyadmin/

    https://gist.github.com/jcavat/2ed51c6371b9b488d6a940ba1049189b

    https://github.com/mzazon/php-apache-mysql-containerized

    https://writing.pupius.co.uk/apache-and-php-on-docker-44faef716150

PHP7

Se for se basear em arquivo `.env` tem que o comando `$ docker-compose` config antes de dar o `$ docker-compose up`

    https://github.com/sprintcube/docker-compose-lamp/tree/7.2.x
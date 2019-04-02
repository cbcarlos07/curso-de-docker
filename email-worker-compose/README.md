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


Docker apache, mysql, php
    
    https://gotechnies.com/docker-compose-yml-mysql-phpmyadmin/

    https://gist.github.com/jcavat/2ed51c6371b9b488d6a940ba1049189b

    https://github.com/mzazon/php-apache-mysql-containerized

    https://writing.pupius.co.uk/apache-and-php-on-docker-44faef716150
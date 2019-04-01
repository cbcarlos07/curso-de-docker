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


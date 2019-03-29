Mostrar o valor padrão de uma variável de ambiente
    
    $ docker container run ex-build-arg bash -c 'echo $S3_BUCKET'
    a chave é nomeada de S3_BUCKET

Gerar uma nova imagem passando argumento para o S3_BUCKET a partir de outra imagem
    
    $ docker image build --build-arg S3_BUCKET=myapp -t ex-build-arg .

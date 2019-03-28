# Curso de docker
https://www.udemy.com/share/1001G2AEYedVtWRXo=/

Entrar na pasta onde se localiza a imagem

Gerar imagem

    $ docker image build -t ex-simple-build .
    -t = significa a tag que eu quero adicionar

Para ver imagem criada
    $ docker image ls

Executar container
    $ docker container run -p 80:80 ex-simple-build    
    -p =  para mapear a porta

Mostrar o valor padrão de uma variável de ambiente
    $ docker container run ex-build-arg bash -c 'echo $S3_BUCKET'
    a chave é nomeada de S3_BUCKET

Gerar nova imagem passando argumento para o S3_BUCKET a partir de outra imagem
    $ docker container build --build-arg S3_BUCKET=myapp -t ex-build-arg .

Acessar o inspect
    $ docker image inspect --format="{{index .Config.Labels \"maintainer\" }}" ex-build-arg

Para parar um container por ID
    $ docker stop CONTAINER_ID
    Não esquecer de substituir o CONTAINER_ID pelo seu código de container
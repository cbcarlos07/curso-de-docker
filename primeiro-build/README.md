Gerar imagem a partir do Dockerfile

    $ docker image build -t ex-simple-build .    
    -t = significa a tag que eu quero adicionar
    $ docker image build -t minha-tag .
    . = minha pasta atual

Executar container
    
    $ docker container run -p 80:80 ex-simple-build 
    -p 80:80=  para mapear a porta. Porta externa: porta interna
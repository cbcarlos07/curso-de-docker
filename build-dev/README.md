Gerar a image

    $ docker image build -t ex-build-dev .
    $ docker image build -t tag_da_image .

Rodar container

    $ docker container run -it -v $(pwd):/app -p 80:8000 --name python-server ex-build-dev

Acessar log de outro container 

    $ docker container run -it --volumes-from=python-server debian cat /log/http-server.log
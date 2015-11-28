# docker-kannel

[Kannel SMS gateway](http://www.kannel.org/) docker image.  
Using sqlbox with postgresql94.

create folder

    mkdir /opt/dockers

then move into it and clone repo into ./kannel

    cd  /opt/dockers
    git clone https://github.com/hlihhovac/docker-kannel.git ./kannel

create docker-compose YML config

    # kannel1.yml
    kannel1:
      build: ./kannel
      dockerfile: Dockerfile.centos7-kannel
      container_name: kannel-1
      mem_limit: 1024m
      memswap_limit: 2048m
      working_dir: /data
      external_links:
        - pgsql-1:pgsql
      volumes:
        - /opt/docker-shared/kannel1/etc:/etc/kannel
        - /opt/docker-shared/kannel1/log:/var/log/kannel
        - /opt/docker-shared/kannel1/spool:/var/spool/kannel
      environment:
      ports:
        - "13000:13000"

finally start container

    docker-compose -f kannel1.yml up -d


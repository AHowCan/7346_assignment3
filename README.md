Austin Canter <br>
CS7346 <br>
Assignment3-400 <br>

Yay, service accounts + Workload identity federation should be working. <br>

I enjoyed learning the additional software development processes like CI/CD and github actions in general.


# A very simple webserver
All credit goes to the original author:
[koind/docker-simple-webserver | Github Repo](https://github.com/koind/docker-simple-webserver)

Furthermore this was used in SMU CS7346 class and homework assignments. 

# Simple web server in docker container

## Built docker image
```sh
$ docker build -t webserver .
```

## Run
```sh
$ docker run -d -p 80:80 webserver
```

## Dokerfile

```dockerfile
FROM debian:9.3-slim

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

RUN apt-get update \
    && apt-get install -y curl

ENV NVM_DIR /usr/local/nvm
ENV NODE_VERSION 8.9.4

RUN curl --silent -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash

RUN source ~/.bashrc && nvm install $NODE_VERSION && nvm alias default $NODE_VERSION && nvm use default

ENV NODE_PATH $NVM_DIR/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

RUN node -v
RUN npm -v

RUN npm install express

COPY . /var/www/html

WORKDIR /var/www/html

EXPOSE 80

CMD node webserver.js
```

 
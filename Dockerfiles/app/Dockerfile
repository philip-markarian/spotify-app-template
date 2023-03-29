FROM node:16

ARG TOKEN

RUN mkdir /myapp
WORKDIR /myapp

# For app
COPY ./app/package.json /myapp/app/package.json
COPY ./app/yarn.lock /myapp/app/yarn.lock

# For functions
RUN mkdir /myapp/functions
COPY ./functions/package.json /myapp/functions/package.json
COPY ./functions/yarn.lock /myapp/functions/yarn.lock

RUN npm --unsafe-perm install -g foreman firebase-tools@9.23.0 jest\
  --cache /tmp/empty-cache \
  && rm -rf /tmp/empty-cache

RUN apt-get update && \
  apt-get install -y openjdk-11-jdk ca-certificates-java ant && \
  apt-get clean;
RUN update-ca-certificates -f;

COPY . /myapp

RUN firebase use default --token=${TOKEN}

CMD ["nf", "start"]

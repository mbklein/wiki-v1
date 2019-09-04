FROM node:8-stretch-slim
LABEL maintainer="requarks.io"

RUN apt-get update -qq && \
    apt-get install -y bash curl git openssl && \
    apt-get clean && \
    mkdir -p /var/wiki && \
    mkdir -p /logs

WORKDIR /var/wiki

COPY . /var/wiki
RUN yarn install && \
    yarn build

ENV WIKI_JS_HEROKU=1

EXPOSE 3000

ADD https://raw.githubusercontent.com/vishnubob/wait-for-it/master/wait-for-it.sh /usr/sbin/wait-for-it
RUN chmod 0755 /usr/sbin/wait-for-it
ENTRYPOINT ["/usr/sbin/wait-for-it", "mongo:27017", "-t", "30", "--", "node"]
CMD ["server"]

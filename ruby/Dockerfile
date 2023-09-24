FROM ruby:3.2.2-alpine3.18

ARG APP_PATH=/usr/src/app
ARG APP_USER=appuser
ARG APP_GROUP=appgroup
ARG APP_GROUP_GID
ARG APP_USER_UID

RUN apk add --update \
        bash \
        build-base \
        tzdata \
        sqlite \
        git && \
      gem install bundler && \
      addgroup -g $APP_GROUP_GID -S $APP_GROUP && \
      adduser -s /sbin/nologin -S -u $APP_USER_UID -G $APP_GROUP $APP_USER && \
      mkdir $APP_PATH && \
      chown $APP_USER:$APP_GROUP $APP_PATH

COPY docker-entrypoint.sh /usr/bin

RUN chmod +x /usr/bin/docker-entrypoint.sh

WORKDIR $APP_PATH

COPY --chown=$APP_USER:$APP_GROUP Gemfile* $APP_PATH/

RUN bundle install

USER $APP_USER

COPY --chown=$APP_USER:$APP_GROUP Gemfile* $APP_PATH/

ENTRYPOINT ["docker-entrypoint.sh"]

EXPOSE 3000

CMD ["rails", "server", "-b", "0.0.0.0"]
#ENTRYPOINT ["tail", "-f", "/dev/null"]
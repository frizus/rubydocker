FROM ruby:3.2.2

RUN bundle config --global frozen 1

WORKDIR /usr/src/app

COPY Gemfile Gemfile.lock ./
RUN bundle install

EXPOSE 3000
CMD ["rails", "server", "-b", "0.0.0.0"]
#ENTRYPOINT ["tail", "-f", "/dev/null"]